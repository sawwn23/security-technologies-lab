# Gnu Privacy Assistant
Gnu Privacy Assistant (GPA) is a graphical program that interfaces with the GnuPG software. It should be noted that I have had several versions of GPA occasionally crash in Windows.

- Step 0 - Prerequisites
Install Gpg4Win from http://gpg4win.org. You want the full version.

You also need your recipient's public key either saved in a file or able to be copied to the clipboard.

- Step 1 - Generate your own keypair

Open GPA. To create a new keypair click Keys --> New Key. Choose a name for the key. Click Forward. Enter an email address. The address doesn't have to be valid. To skip the email address, enter some text in the box and delete it. The Forward button will still be clickable. Click Forward. Feel free to select create a backup copy. [It's not necessary, but it's a good idea if the key is important] Click Forward. GPA will ask your for a passphrase for this key. Choose one that you've never used before and WRITE IT DOWN. After verifying the passphrase, GPA will generate the key and it will show up in the main window (Key Manager) of GPA.

- Step 2 - Import your recipient's public key.

To encrypt a message, you need your recipient's public key. Find it and save the whole thing to a file. Make sure to select and save the whole key, including the -----BEGIN PGP PUBLIC KEY BLOCK----- and -----END PGP PUBLIC KEY BLOCK-----. All of it is necessary. Once saved, import the key to GPA. (Keys --> Import Keys) GPA should tell you that one public key was imported.

- Step 3 - Compose your message

Open up a text editor. (Notepad is fine) Type your message. This is what your recipient will see. Save the message to a file.

- Step 4 - Encrypt your message

GPA can work with files or text as inputs. You can use a text editor to write your message, save it as a file and GPA can work with the file. To work with a file, click Window --> File Manager in GPA. You could also work with text directly. To work with text in GPA, click Window --> Clipboard. The encryption procedure is the same for both.
Add a file to the File Manager by clicking File --> Open and selecting your file. To add text to the Clipboard, simply type your message or use another text editor and copy/paste your message into the Clipboard. Once you have your message in GPA, click File --> Encrypt (In the File Manager or Clipboard window) to begin the encryption process. In the window that opens, select your recipient's key. You can select multiple recipients by holding down CTRL and selecting multiple keys. You can also select yourself so that you can decrypt the message. After your select your recipients, make sure you select the Armor checkbox. This formats the encrypted message as random letters and numbers. Click OK and GPA will encrypt your message.

If your message was a file, then the encrypted file will be in the same location as the original file and will have the same filename but it will have a .asc file extension. That file contains your encrypted message. Open it with a text editor to view it. If you used the Clipboard, your original message will turn into the encrypted message. It will start with -----BEGIN PGP MESSAGE----- and the rest will be gibberish.

- Step 5 - Send your encrypted message to your recipient

Your encrypted message looks like gibberish. And it IS gibberish to everyone except the people you added as recipients. The recipients can decrypt the message back into text. Nobody else can. You can send the encrypted message in an email or post it anywhere. The contents of your message are safe.

If you want your recipient to be able to send encrypted messages that you can read, make sure to include your own public key. To do this, select your own key in GPA and click Keys --> Export Keys. (You can also right click the key and select Export Keys) Save the file under any name. Send the file to your recipient or copy the text inside the file and send that. Your public key can also be freely given out.

- Step 6 - Receive an encrypted response and decrypt it

Your recipient will receive your encrypted message and your public key. He or she will decrypt the message and then use your public key to create an encrypted message to you. (The same process that you just completed) Once you receive an encrypted message from your recipient you will need to decrypt it so you can read it. Save the encrypted message as a file or copy it. (Ctrl + C)

Similar to before, if your encrypted message from your recipient is a file, click Window --> File Manager and then File --> Open to select the encrypted file. If your encrypted message from your recipient is in an email or webpage, select it and copy/paste it into GPA's Clipboard (Window --> Clipboard). To decrypt the message, Click File --> Decrypt. GPA will then ask you for your password to your key. Since you WROTE IT DOWN just type the password and click OK. GPA's File Manager will save the plaintext file in the same place as the encrypted file. GPA's Clipboard will convert the encrypted text to plaintext right in the Clipboard window.
