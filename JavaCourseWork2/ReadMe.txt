Specification
Overview
Write a program that encrypts or decrypts the contents of a text file using a secret keyword.  Additionally, your program should analyse the frequency of occurrence of each alphabetic character in the encrypted or decrypted file that is produced.  The first part of the exercise uses a simple encryption strategy known as a monoalphabetic cipher, whilst the second part uses a more sophisticated strategy called the Vigenère cipher.
Text files
Your program will work with three types of input text files.  The plaintext file (P) is the original English file before encryption, the cipher text file (C) is the encrypted file and the deciphered file (D) is the result of decrypting the cipher text file.  If your program works then the P and D files will be identical!

The three files will have filenames of the form messageP.txt, messageC.txt and messageD.txt, where the root filename message can change.

All the text in the plaintext file must be in capitals.  Any characters such as spaces and punctuation are not encrypted.  This means that the cipher text contains the same number of words (and the same punctuation) as the original text, each with the same number of letters, (which would be a help for a code breaker).
Keyword
The keyword is a single word that is used to generate the monoalphabetic or Vigenère cipher.  It must not contain any duplicate letters.  It will be typed into the GUI.  The letters must be in capitals.
Sample Input/Output
The following cipher text is produced by the Vigenère cipher:

Keyword:
LEOPARD

Plaintext:		       Cipher Text:
THE MAN WHO MAKES NO 
MISTAKES DOES NOT 
USUALLY MAKE ANYTHING
EDWARD JOHN PHELPS		ELS BAE ZSS APKVV YS 
AXSKDVIG SOVV YSH 
JSLDWPM BABH LRMIHZQR
IRLAIG USVC PYHWTG

Letter Frequencies
The second output file will contain a report based on the text file that is produced as a result of the relevant encryption / decryption operation (i.e., based on the text in the C or D file respectively).  The name of this second output file will be identical to the root filename, but with the letter F appended (e.g., messageF.txt).  The contents of this report will be a table consisting of, for each letter of the alphabet:

1.	the letter itself;
2.	the frequency (the number of times it occurs in the file);
3.	the frequency percentage (the frequency divided by the total number of alphabetic characters in the file, given as a percentage), to 1 decimal point;
4.	the percentage frequency of the letter shown for an average English language document (these values are provided for you);
5.	the difference between the percentages in columns 3 and 4.

Finally the letter with the maximum frequency should be displayed, together with its frequency percentage.  If several letters have the same frequency, only the last letter (i.e., the one furthest down in the alphabet) should be displayed.  The objective of this report is to show how close the letter frequencies in the output file are to those in an average English language document; this provides some indication as to the strength of the encryption.

The numbers displayed in the report should be lined up in columns, as illustrated by the following sample report:

LETTER ANALYSIS

Letter  Freq  Freq%  AvgFreq%  Diff
   A    34     7.6     8.2    -0.6
   B    12     2.7     1.5     1.2
   C    19     4.3     2.8     1.5
   D     9     2.0     4.3    -2.3
   E    55    12.4    12.7    -0.3
  ...
   Y    16     3.6     2.0     1.6
   Z     0     0.0     0.1    -0.1

The most frequent letter is E at 12.4%

(Note that it should not be necessary to read back in the text file that is produced as a result of the encryption / decryption operation in order to produce the letter frequencies report.)

The GUI
Code to display the GUI shown below at the start of the program is supplied for you in the CipherGUI class.  The GUI functionality will be governed by this class.  

The textfields are used to enter the keyword and the name of the input text file.  Since all filenames will end with “.txt”, this suffix can be omitted at this stage, and added within the code.  Buttons are used to choose which style of cipher to use, i.e., monoalphabetic or Vigenère cipher.  (Full details of the encryption and decryption mechanisms for each of these ciphers are given below.)
Program Functionality
When a button is clicked, the keyword should be checked to ensure that it is valid.  That is, it should be non-empty, and should contain only upper-case letters of the alphabet with no repeated character.  Similarly, the validity of the filename should be checked, ensuring that it ends with either ‘P’ or ‘C’ (remember that “.txt” should be omitted).  If either the keyword or the filename is invalid, then an error message should be displayed using JOptionPane, and the relevant textfield should be cleared, allowing the user to try again.

Otherwise the program will proceed to the encryption phase (if a filename ending in ‘P’ is entered, signifying that the user wishes to encrypt a plaintext file) or the decryption phase (if a filename ending in ‘C’ is entered, signifying that the user wishes to decrypt a previously encrypted file) and produce the frequency analysis.  Any input/output exceptions (such as file not found) should be caught and handled with a JOptionPane error message, allowing the user to re-enter the filename.
Encrypting and decrypting
To encrypt the text, a cipher must initially be created.  There are two ciphers that can be used, both based on a keyword – a simple monoalphabetic cipher and the Vigenère cipher.  The GUI contains two buttons, and the user chooses which cipher to use after having entered the keyword and the text file.

Initially you should create a program that only works with the monoalphabetic cipher, and then go on to the Vigenère cipher if you have time.  In addition to normal program use, each cipher array should be printed to System.out so that you (and your tutor) can verify that it has been created correctly.

It is not expected that the program should make any check that, upon decrypting a file, the user enters the same keyword and type of cipher that was used in order to initially create the encrypted file.

The ciphers are now described in more detail:
The monoalphabetic cipher
This uses two parallel arrays.  The first is an array containing the letters of the alphabet in order.  In the encryption array, the letters of the alphabet are arranged starting with the keyword and followed by the remaining letters in reverse order.  To encrypt a character, you can calculate the index position of the character within the normal alphabet on the top line, by subtracting the value ′A′ from the character.  The encrypted character is then the one in the corresponding position (with the same index) in the lower array.  To decrypt a character, it is necessary to search for the character in the lower encryption array to find the index, before obtaining the corresponding character from the array on the top line.
The Vigenère cipher
This uses several different cipher text arrays, one for each letter in the keyword.  Thus you will need an array of arrays (a 2D array) to store the different encryption arrays.

Each row of the encryption arrays starts with one letter of the keyword followed by the remaining letters of the alphabet in order, with A following Z.  Thus there will be one encryption array for each letter in the keyword.  You can assume that the keyword will not contain more than 26 letters!

Suppose the keyword is of length n.  The first character to be encrypted is coded with reference to the first encryption array, the second using the second array, etc.  The (n+1)th character uses the first encryption array again (because the keyword has only n letters), and so the cycle continues.  Decryption uses a similar idea: the first character is decoded with reference to the first encryption array, and so on, cycling back to the first array when the (n+1)th character is reached.


