Title:Print(Minecraft)
Date: 2013-1-12 8:20

Now that my Pi is running smoothly and playing Pandora from the command line I needed to find another project. I enjoy minecraft on xbox so I though I would give Minecraft Pi a chance. Minecraft Pi is officially unreleased, but an officially acknolewdged unofficially leaked version is floating around the [minecraft forums](http://www.minecraftforum.net/topic/1587033-minecraft-pi-features-and-news-pre-release-leaked/). 

After creeping the forums for a bit I managed to get minecraft installed and running as well as get a basic python script hooked in to my minecraft session. Once I figured out how to place blocks I took the next logical step and decided to write messages in the Minecraft sky. Although this was my first experience with python I was able to go from concept to executable in about 4 hours. I will now work only in python for perpetuity. 

The sky-writing script only does two things...


Defining how leters are made:

Using an imaginary 3x5 grid where each pixel is numbered from bottom left to top right, a character can be defined as a list of numbers. So the letter E becomes

	:::py3
	E = [1,2,3,4,7,8,10,13,14,15]

Then a general letter-drawing function can place blocks in the numbered spaces called out in the letter list. 

	:::py3
	if 1 in Letter:
		a.setBlock(x,y,z,blockID)
	if 2 in Letter:
		a.setBlock(x+1,y,z,blockID)
	if 3 in Letter:
		a.setBlock(x+2,y,z,blockID)

and so on...


Deciding where to draw the letters:

Although drawing letters is fun, it's only useful if the letters make up readable words. There is a tradeoff between the resolution of characters (number of blocks per letter) and the number of letters than can fit in a player's view in Minecraft. I quickly figured out that the smallest grid that would support the largest percantage of numbers was a 3x5. So that means that with 1 space in between letters, a player could see about 18 characters (18*(3+1)=72 blocks). With a line heigth (5) and a line width (18 chars) I set up a function to decide where to draw words. 

	:::py3
	def parseString(sinput,x,y,z,blockID):
	#Break string into words, decide where to place each word and letter	
		#Set z height of top line and number of chars per line
		topline = 50
		linewidth = 15	

		line = 0          #line number
		characters = 0	  #number of characters already on the line
		words = sinput.lower().split(" ")
		for word in words: #for each word in the string
			if (characters + len(word)) > linewidth:  #the word is too long for the current line
				#clear rest of line, move to the next line, reset characters count	
				a.setBlocks(x+characters*4,topline-7*line,z,x+linewidth*4,topline-7*line+5,z,0)
				line = line + 1
				characters = 0	
			for letter in word:  #for each character in the current word
				if letter == '\n':  #start on the next line
					#clear rest of line, move to next line, reset characters count
					a.setBlocks(x+characters*4,topline-7*line,z,x+linewidth*4,topline-7*line+5,z,0)
					line = line + 1
					characters = 0
				else:
					try:    #drawing the letter
						drawLetter(abc[letter],x+characters*4,topline-7*line,z,blockID)
					except: #When the letter is not in dict abc[], draw a blank
						drawLetter(abc[' '],x+characters*4,topline-7*line,z,blockID)
					characters = characters + 1	
			#After each word
			drawLetter(blank, x+characters*4, topline-7*line, z, blockID)
			characters = characters + 1
		#After all words are drawn, clear the rest of the current line and the next line
		a.setBlocks(x+characters*4,topline-7*line,z,x+linewidth*4,topline-7*line+5,z,0)
		line = line + 1
		a.setBlocks(x+characters*4,topline-7*line,z,x+linewidth*4,topline-7*line+5,z,0)

The x,y,z inputs are a starting location for the bottom left corner of the first character drawn. 

Once this module is imported and a minecraft session is open, any string can be turned into blocks in Minecraft. How useful the program is, well... it's a fun way to play with python!

	
