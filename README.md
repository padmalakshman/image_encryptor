@ -0,0 +1,58 @@
def encrypt_image(image_path, encrypted_image_path, key):
    """
    Encrypt an image by swapping red and blue pixel values and adding a key to each pixel value.
    """
    try:
        image = Image.open(image_path)
        pixels = list(image.getdata())
        encrypted_pixels = [(pixel[2], pixel[1], pixel[0]) for pixel in pixels]
        encrypted_pixels = [(pixel[0] + key, pixel[1] + key, pixel[2] + key) for pixel in encrypted_pixels]
        encrypted_image = Image.new(image.mode, image.size)
        encrypted_image.putdata(encrypted_pixels)
        encrypted_image.save(encrypted_image_path)
        print("Image encrypted successfully!")
    except Exception as e:
        print("Error encrypting image:", str(e))

def decrypt_image(encrypted_image_path, decrypted_image_path, key):
    """
    Decrypt an encrypted image by subtracting the key from each pixel value and swapping red and blue pixel values again.
    """
    try:
        image = Image.open(encrypted_image_path)
        pixels = list(image.getdata())
        decrypted_pixels = [(pixel[0] - key, pixel[1] - key, pixel[2] - key) for pixel in pixels]
        decrypted_pixels = [(pixel[2], pixel[1], pixel[0]) for pixel in decrypted_pixels]
        decrypted_image = Image.new(image.mode, image.size)
        decrypted_image.putdata(decrypted_pixels)
        decrypted_image.save(decrypted_image_path)
        print("Image decrypted successfully!")
    except Exception as e:
        print("Error decrypting image:", str(e))

def main():
    while True:
        print("Image Encryption Tool")
        print("1. Encrypt Image")
        print("2. Decrypt Image")
        print("3. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            image_path = input("Enter the path to the image to encrypt: ")
            encrypted_image_path = input("Enter the path to save the encrypted image: ")
            key = int(input("Enter the encryption key: "))
            encrypt_image(image_path, encrypted_image_path, key)
        elif choice == "2":
            encrypted_image_path = input("Enter the path to the encrypted image to decrypt: ")
            decrypted_image_path = input("Enter the path to save the decrypted image: ")
            key = int(input("Enter the decryption key: "))
            decrypt_image(encrypted_image_path, decrypted_image_path, key)
        elif choice == "3":
            print("Exiting the program. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
