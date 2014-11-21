CryptoPPJava
============

##Description
This application is a port from the CryptoPP library v5.6.2 for the classes
DefaultEncryptorMAC and DefaultDecryptorMAC to java

This was made primarily because there was no way to decrypt the CryptoPP DefaultEncryptorwithMAC in a way that was
cross-platform.

If you see any issues, feel free to submit a pull request!

##Requirements

Include the following jars on your build path (or find reputable alternatives)
Note that you can drop the commons dependencies (especially codec) if you alter a few
functions as they are primarily used out of convenience.
* <a href="http://www.bouncycastle.org/latest_releases.html">Bouncy Castle for JDK 1.5-1.7</a>
* <a href="http://commons.apache.org/proper/commons-io/">Apache Commons IO</a>
* <a href="http://commons.apache.org/proper/commons-codec/">Apache Commons Codec</a>

##Usage

The examples are included in the files in the main method.  They are included below for convenience:

      	public static void main(String[] args) throws Exception {
      		if (args.length != 2) {
      			System.out.println("Usage: java DefaultEncryptorWithMAC text password");
      			System.exit(1);
      		}
      		DefaultEncryptorDecryptorWithMAC encoderDecoder;
      		if (args.length == 2) {
      			encoderDecoder = new DefaultEncryptorDecryptorWithMAC();
      			begin(args[0], args[1], encoderDecoder);
      		} else {
      			System.out.println("Invalid arguments");
      		}
      	}
      	


      	public static void begin(final String text, final String password, DefaultEncryptorDecryptorWithMAC encoderDecoder) throws Exception {
      
      		System.out.println("Original String: ");
      		System.out.println("\t" + text);
      
      		//Use predefined key
      		System.out.println("Key: \t" + password);
      
      		byte[] encryptedText = encoderDecoder.encrypt(text.getBytes(), password);
      		FileOutputStream fos = new FileOutputStream(new File("encrypted.bin"));
      		fos.write(encryptedText);
      		fos.flush();
      		fos.close();
      		System.out.println(encryptedText.length);
      		System.out.println("Encrypted Text Hex Encoded: \n\t" + 
      				new String(Hex.encodeHex(encryptedText)) + "\n" );
      
      		ByteArrayOutputStream out = new ByteArrayOutputStream();
      		FileInputStream in = new FileInputStream("encrypted.bin");
      		IOUtils.copy(in, out);
      		byte[] b = out.toByteArray();
      		in.close();
      		out.close();
      		byte[] decryptedText = encoderDecoder.decrypt(b, password);
      
      		System.out.println("Original Text Decrypted: ");
      		System.out.println("\t" + new String(decryptedText));
      	
      	}
