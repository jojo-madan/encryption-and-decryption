# encryption-and-decryption
#!/bin/bash

# Step 1: Create a file
echo "This is a sample file created at $(date)" > file.txt

# Step 2: Generate a digital signature
openssl dgst -sha256 -sign ststemA_private.key -out file.sig file.txt

# Step 3: Encrypt the file and signature with the receiver's public key
openssl rsautl -encrypt -inkey systemB_public.key -pubin -in file.txt -out encrypted_file.txt
openssl rsautl -encrypt -inkey systemB_public.key -pubin -in file.sig -out encrypted_file.sig

# Step 4: Decrypt the data after transfer (assuming you're simulating both ends)
openssl rsautl -decrypt -inkey systemB_private.key -in encrypted_file.txt -out decrypted_file.txt
openssl rsautl -decrypt -inkey systemB_private.key -in encrypted_file.sig -out decrypted_file.sig

# Step 5: Verify the signature
openssl dgst -sha256 -verify systemA_public.key -signature decrypted_file.sig decrypted_file.txt
                                                                                                 
