# Práctica 3a. GPG Pretty Good Privacy

## Contexto
El término criptografía proviene del griego *kyptós* 'oculto' y *grafé* 'escritura' y es definida como el arte de escribir con clave secreta o de un modo enigmático.

Gracias al uso de la criptografía se puede obtener una seria de ventajas de gran utilidad en el ámbito de la seguridad informáticfa como son:
* Confidencialidad
* Integridad
* Autenticidad
* No repudio
    

En esta práctica se trabajará sobre estos cuatro conceptos mediante la herramienta de comandos gpg (Pretty Good Privacy)

## Objetivos
* Entender la *confidencialidad, Integridad, Autenticidad* y no repudio mediante el uso de la herramienta *gpg*.
* Entender y poner en práctica la criptografía simetrica
* Entender y poner el práctica la criptografía asimétrcia
* Saber cifrar y descifrar mensajes mediante criptografía simétrica.
* Saber cifrar y descifrar mensajes mediante criptografía asimétrica.
* Saber firmar otras llaves generando así una relación de confianza entre usuarios de la comunidad.
* Ser capaces de firmar un documento y verificar que este ha sido firmado por quien dice ser.
* Ser capaces de importar/exportar claves a un servidor público
* Saber enviar correos cifrados y descifrar correos privados

## Desarrollo

 1. **Cifrar y descifrar un mensaje mediante criptografía simétrica**

Texto cifrado "asir2"
```bash
echo "texto plano" | gpg --symmetric --armour --batch --passphrase asir2
```
```bash
-----BEGIN PGP MESSAGE-----

jA0ECQMCoxc4/JdrBuv/0kEBa4wRz4uAm3W0mfTH7a1PThwogtHdHE8ewKnJEU4H
b5hUzQABRaR4yxVIUw4nIh8ya6Qm4H12VD0U6oO4SSUBlg==
=Lp5r
-----END PGP MESSAGE-----
```
 1. **Crear par de claves**
```bash
gpg --full-gen-key
```
 1. **Listar claves pública/privada**
```bash
/root/.gnupg/pubring.kbx
------------------------
sec   rsa3072 2024-12-02 [SC]
      252B49B93EA2A2EDB290DD8A33E041D903FC48B1
uid           [ultimate] Vinicio <vinatasal@alu.edu.gva.es>
ssb   rsa3072 2024-12-02 [E]
```
 2. **Importar/exportar claves publicas y privadas**
```bash
gpg --import public_key.asc
gpg --import private_key.asc

```
```bash
gpg --export --armour vinatasal@alu.edu.gva.es > public_key.asc

gpg --export-secret-key --armour vinatasal@alu.edu.gva.es > secret_key.asc

gpg --export --armour > all_public_keys.asc

gpg --export-secret-keys --armour > all_private_keys.asc
```
 3. **Importar y exportar de un servidor de claves**

Exportar
```bash
Gpg --keyserver keyserver.ubuntu.com --send-keys
```
Importar
```bash
Gpg --keyserver keyserver.ubuntu.com --receive-keys
```
 1. **Encriptar un documento con clave pública de destinatario**
```bash
gpg --encrypt --recipient *email_del_destinatario/ID_DE_LA_CLAVE* --armour documento.txt

gpg --encrypt --recipient *email_del_destinatario/ID_DE_LA_CLAVE* --armour  --output documento.txt.asc
```

 2. **Desencriptar un documento cifrado con nuetra clave publica haciendo uso de clave privada**
```bash
gpg --decrypt encriptao.txt.asc

gpg --decrypt --output desencriptao.txt encriptao.txt.asc
```
 3. **Firmar un mensaje y verificar la autoria de un mensaje**
```bash
gpg --clear-sign firmar.txt
gpg --local-user vinatasal@alu.edu.gva.es --clear-sign firmar.txt

gpg --verify firmar.txt.gpg
gpg --verify firmar.txt.asc
```
 4.  **Mailvelope**
    1.  Importar clave privada
    2.  Subir clave pública al keyserver de mailevelope
```
Vamos a esta página

chrome-extension://kajibbejlbohfaggdiogboambcijhkke/app/app.html#/keyring/import 

y subimos la clave
```
    3.  Importar claves publicas
    4.  Enviar un mensaje cifrado y descifrar mensaje.

 