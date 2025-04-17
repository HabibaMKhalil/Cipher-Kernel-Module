## 🔐 CIPHER KERNEL MODULE (RC4 ENCRYPTION)
Linux Kernel | RC4 Cipher | Character Device | Proc Interface                                                         
A kernel module implementing RC4 encryption/decryption 
with dual interface (character device + proc filesystem).

## 🚀 KEY FEATURES

✔ RC4 stream cipher implementation                                      
✔ Dual interface: /dev/cipher + /proc/cipher                                 
✔ Real-time kernel logging via pr_info                                 
✔ Secure key handling in kernel space                                                      

## 🛠️ PREREQUISITES
$ sudo apt install linux-headers-$(uname -r) gcc make                             

## ⚡ QUICK START
1. Compile and load module                       
$ make                        
$ sudo insmod cipher_module.ko                                                       

2. Verify loading                  
$ dmesg | tail -3                  
[ 1234.5678] Initializing cipher module                       
[ 1234.5679] Allocated major number: 123                  
[ 1234.5680] Cipher module loaded             

3. Set key and encrypt                      
$ echo "SECRET_KEY" > /dev/cipher_key                
$ echo "Plaintext" > /dev/cipher              

4. Read encrypted output               
$ sudo cat /dev/cipher               
> ��%�jM�               


## 📂 FILES & INTERFACES
/dev/cipher        - Write msgs/keys, read encrypted data                   
/dev/cipher_key    - Key input (alternate)                   
/proc/cipher       - Read decrypted messages                 
/proc/cipher_key   - Key input for decryption                                 

💡 EXAMPLE WORKFLOW
1. Set Key                   
$ echo "kernel123" > /dev/cipher_key                       

2. Encrypt                
$ echo "SecurityRocks" > /dev/cipher                
 
3. Read Ciphertext                   
$ cat /dev/cipher                       
> �x$�q�Z�             

4. Decrypt                   
$ echo "kernel123" > /proc/cipher_key                    
$ cat /proc/cipher                        
> SecurityRocks                              

## ⚠️ SECURITY NOTES
🔒 Keys remain in kernel memory until module unload
📝 Prefer /proc interface for sensitive operations
🚫 RC4 has known vulnerabilities - not for production
