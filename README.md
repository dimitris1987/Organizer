# Individual Assignment 1

## Question 1
The program takes 4 arguments, all required. For more help you can run the app with -h or --help argument.\
`python3 caesar.py -h` or\
`python3 caesar.py --help`

The program accepts both short and long arguments\
`-i INPUT, --input INPUT`\
`-o OUTPUT, --output OUTPUT`\
`-k KEY, --key KEY`\
`-m MODE, --mode MODE`

Here are some valid ways that we can call the program\
`python3 caesar.py -i input.txt -o output.txt -k 8 -m enc`\
`python3 caesar.py --input input.txt -o output.txt -k 8 -m enc`\
`python3 caesar.py --input input.txt -o output.txt --key 8 -m enc`\
`python3 caesar.py --input input.txt --output output.txt --key 8 --mode enc`
All above commands with an inputfile containing the text "hello WORLD", will generate an output file "output.txt" with content "PMTTWEWZTL"\
At the same time, all above commands with mode 'dec' instead of 'enc', and input content "PMTTWEWZTL" will generate the "output.txt" with content 'HELLOWORLD"

The `caesar.py` is called, 4 functions are executed.
* The first function `take_command_line_args` reads the command line arguments. Between `argparse`, `optparse`, and `getopt` libraries I chose to go with `argparse` because to my point of view, has better argument handling and validation. It accepts 4 arguments, 3 strings and 1 integer (key). I defined `type=int` to take advantage of the argparse validation tool. The function returns the arguments.
* Next, `validate_arguments` function is executed. Here i want to validate the mode argument. The value of this argument can be 'enc' or 'dec'. The function check if mode argument value holds any of these 2. If it has any other value, it throws an error and terminates the program.
* Next, `read_input` function is called, which reads the input file and returns it content. Since the cipher is case insensitive, I convert the content of file to uppercase and i remove the empty spaces (`.upper().replace(" ", "")`). If input file does not exist, it throws an error and terminates the program.
* Last, the `substitute` function is executed, which accepts as parameters the returned content of input file, and the user arguments. The functions starts, by initializing an empty string `new_text` which will hold the encrypted or decrypted message that is going to be written in the output file. Next, I iterate every single character of the input text, and check if the character exist in the `alphabet`. The alphabet is a predefined string that contains the upper case letters of the English alphabet. If a character is not included in the alphabet (if index == -1), then an error message is thrown, and program ends. If exists, it finds the `index` of the alphabet (A=0, B=1, ...). Next, depending the mode, it computes the new Index (`new_index`). In case of encryption, new index equals `(index + args.key) % 26`, otherwise index equals `(index - args.key) % 26`. The modulus operation is performed with the number 26, since the alphabet has 26 letters. Having the new index, we have also the new subtituted character, which is appended to `new_text (new_text += alphabet[new_index])`. When the for loop finishes, we have the subtituted message, so I write it to the output file, printing a message to user. It is mentioned here, that the `substitute` function is the same for both encryption and decryption.

