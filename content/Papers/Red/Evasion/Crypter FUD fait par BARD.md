```cpp
#include <stdio.h>
#include <stdlib.h>
#include <openssl/aes.h>

int main(int argc, char **argv) {
  // Lire le code malveillant
  FILE *fp = fopen(argv[1], "rb");
  if (fp == NULL) {
    printf("Erreur lors de l'ouverture du fichier\n");
    return 1;
  }

  // Choisir un algorithme de cryptage
  const EVP_CIPHER *cipher = EVP_aes_128_cbc();

  // Créer une fonction de cryptage
  void encrypt(unsigned char *data, size_t size) {
    // Initialiser le chiffrement
    EVP_CIPHER_CTX *ctx = EVP_CIPHER_CTX_new();
    EVP_EncryptInit_ex(ctx, cipher, NULL, NULL, NULL);

    // Crypter les données
    int len = 0;
    unsigned char *out = malloc(size);
    while (len < size) {
      int outlen = 0;
      EVP_EncryptUpdate(ctx, out + len, &outlen, data + len, size - len);
      len += outlen;
    }

    // Terminer le chiffrement
    EVP_EncryptFinal_ex(ctx, out + len, &outlen);
    EVP_CIPHER_CTX_free(ctx);

    // Remplacer les données originales par les données cryptées
    memcpy(data, out, len);
    free(out);
  }

  // Crypter le code malveillant
  unsigned char *data = malloc(1024);
  fread(data, 1, 1024, fp);
  encrypt(data, 1024);

  // Sauvegarder le code crypté
  FILE *fpout = fopen("malware.crypted", "wb");
  fwrite(data, 1, 1024, fpout);
  fclose(fpout);

  // Fermer le fichier
  fclose(fp);

  return 0;
}
```
