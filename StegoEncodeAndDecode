#Import the required modules, some of this modules are not existed in the default python liberaries and need to be installed, check the readme file on how to install them.
from PIL import ImageTk, Image
# this module need to be installed
import math,string
import os, random



def enc(image, msg):
    
    # insert the text file and the cover image, and then check if is it possible to embbed the text inside the cover, if the text is bigger an error will come to the python interface. if that not the case the function will use ord() to unicode the letters (the text file), and using the pil liberary to insert the image, and then seprating each pixel to three rows and each row contains a 8 bit coloumn ( the three colours; red, green and blue), then replacing the last bit of each coloum by each bit of the text file respectvley, the result of this replacing is saved in the variable new_image and after completing the process the new_image will produce new file using image.save
    #

    
    msg = "." + msg
    width, height = image.size
    if (width * height) < len(msg):
        raise ValueError
    pixels = image.load()
    for i in range(0, len(msg)):
        encodedChar = str(ord(msg[i]))
        row = math.ceil(i/float(width))
        column = i%width
        pixel = pixels[row-1, column-1]
        newPixel = list(pixel)
        newPixel[0] = str(newPixel[0])
        newPixel[1] = str(newPixel[1])
        newPixel[2] = str(newPixel[2])

        if ord(msg[i]) >= 100:
            r = list(newPixel[0])
            r[-1] = encodedChar[0]
            newPixel[0] = ''.join(r)

            r = list(newPixel[1])
            r[-1] = encodedChar[1]
            newPixel[1] = ''.join(r)

            r = list(newPixel[2])
            r[-1] = encodedChar[2]
            newPixel[2] = ''.join(r)

        elif ord(msg[i]) >= 10:
            r = list(newPixel[0])
            r[-1] = '0'
            newPixel[0] = ''.join(r)

            r = list(newPixel[1])
            r[-1] = encodedChar[0]
            newPixel[1] = ''.join(r)

            r = list(newPixel[2])
            r[-1] = encodedChar[1]
            newPixel[2] = ''.join(r)

        else:
            r = list(newPixel[0])
            r[-1] = '0'
            newPixel[0] = ''.join(r)

            r = list(newPixel[1])
            r[-1] = '0'
            newPixel[1] = ''.join(r)

            r = list(newPixel[2])
            r[-1] = encodedChar[0]
            newPixel[2] = ''.join(r)


        newPixel[0] = int(newPixel[0])
        newPixel[1] = int(newPixel[1])
        newPixel[2] = int(newPixel[2])
        pixels[row-1, column-1] = tuple(newPixel)
    row = math.ceil(len(msg)/float(width))
    column = len(msg)%width
    pixel = pixels[row, column]
    newPixel = list(pixel)
    newPixel[0] = str(newPixel[0])
    newPixel[1] = str(newPixel[1])
    newPixel[2] = str(newPixel[2])

    r = list(newPixel[0])
    r[-1] = '1'
    newPixel[0] = ''.join(r)

    r = list(newPixel[1])
    r[-1] = '2'
    newPixel[1] = ''.join(r)

    r = list(newPixel[2])
    r[-1] = '7'
    newPixel[2] = ''.join(r)



    newPixel[0] = int(newPixel[0])
    newPixel[1] = int(newPixel[1])
    newPixel[2] = int(newPixel[2])
    pixels[row-1, column-1] = tuple(newPixel)
    imageName = name_image(6)
    imageName = imageName+ ".png"
    image.save(imageName)
    print("Generated stego image is located:",os.path.abspath(imageName))


def decodeMessage(image):
  # here is the function to recover the text from the stego image in first it take the image and loaded to the code using pil liberary and then taking the last bit of each 8 bits in loop cycle until finishing, then taking these binary results and convert it to encoded to utf-8
  
    pixels = image.load()
    encodedText = ""
    for w in range(0, image.size[0]):
        for h in range(0, image.size[1]):
            pixel = pixels[w,h]
            encodedChar = int(str(pixel[0])[-1]) * 100 + int(str(pixel[1])[-1]) * 10 + int(str(pixel[2])[-1])
            if(encodedChar == 127):
                return encodedText
            else:
                encodedText+=chr(encodedChar)
    return encodedText
    
def name_image(length):
   
    return ''.join(random.choice(string.ascii_letters) for k in range(length))

def main():
            
    # interface function when the client can chose to hide or recover text from/in a message
    while True:
        choice = input("Do you want to decode or encode? (d/e) or (q) to quit: ")
        while not(choice == 'd' or choice == 'e' or choice == 'q'):
            print("\n[ERROR] Invalid choice, please input 'd' or 'e'!")
            choice = input("\nDecode or Encode? (d/e): ")
        print()
        if(choice == 'd'):
            file = input('Please provide an image: ')
            data = decodeMessage(Image.open(file))
            if data:
                #save to a file
                out = name_image(5)
                out = out+'.txt'
                with open(out, 'w', encoding="utf-8") as f:
                    f.write(data)
                print('Extracted data was saved in: ',os.path.abspath(out))
            else:
                print("No text found")
                    

            
            
        elif (choice == 'q'):
            exit()
        else:
            image = input('Enter an Image: ')
            msg =  input('Enter a file: ')
            try:
                file = open(msg, 'r').read()
                #file = file.strip()
            except Exception as e:
                print (str(e))
            enc(Image.open(image), file)

if __name__== "__main__":

    main()
