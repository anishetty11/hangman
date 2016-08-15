import random
import re
import sys

HANGMANPICS = ['''



   +---+

   |   |

       |

       |

       |

       |

 =========''', '''

 

   +---+

   |   |

   O   |

       |

       |

       |


 =========''', '''



   +---+

   |   |

   O   |

   |   |

       |

       |

 =========''', '''

 

   +---+

   |   |

   O   |

  /|   |

       |

       |

 =========''', '''

 

   +---+

   |   |

   O   |

  /|\  |

       |

       |

 =========''', '''

 

   +---+

   |   |

   O   |

  /|\  |

  /    |

       |

 =========''', '''

 

   +---+

   |   |

   O   |

  /|\  |

  / \  |

       |

 =========''']
word = 'ant baboon badger bat bear beaver camel cat clam cobra cougar coyote crow deer dog donkey duck eagle ferret fox frog goat goose hawk lion lizard llama mole monkey moose mouse mule newt otter owl panda parrot pigeon python rabbit ram rat raven rhino salmon seal shark sheep skunk sloth snake spider stork swan tiger toad trout turkey turtle weasel whale wolf wombat zebra'.split()
# to find the occurence of a particular letter in a string #
def findSectionOffsets(text):
	global inputs
	global increment
	global counter
	global occurence
	#print "\ncounter=",counter
	guessed_letter=raw_input("\nEnter your guess: \n")
	# to prevent re-entering of the same letter
	if (inputs.count(guessed_letter)>0):
		print "\nPlease enter a different letter"
		findSectionOffsets(selected)
	inputs.append(guessed_letter)
	# to prevent entering more than 1 letter
	if (len(guessed_letter)!=1):
		print "\nPlease enter a single letter"
		findSectionOffsets(selected)
	
	if (selected.count(guessed_letter)==0):
		increment+=1
# append the index where letter matches into occurence[]
	for m in re.finditer(guessed_letter,text):
		n=m.start(0)
		#print "n=",n
		occurence.append(n)	
	#print occurence
# replace the underscore in the empty string by the guessed letter if correct#
	for j in occurence:
		guess[j]=guessed_letter
	for i in range (len(selected)):
		print guess[i],
	
	occurence=[]
	counter+=1
	#print "length",len(selected)
	if (increment<6):
		print HANGMANPICS[increment]
	else:
		print HANGMANPICS[6],"\n \n \tHangman is DeadYou, \n \n \thave lost the match\n \n",
		print "\tThe answer is",selected.upper(),"\n \n"
		# sys.exit() to end the program
		sys.exit()
		# .join(set()) is used to replace multiple occurence into single
	if (guess.count('_')==0):
		print "\n \t Congradulations, Task completed, You made", counter-len(''.join(set(selected))), "\n \t wrong guesses\n \n"
	else:
		findSectionOffsets(selected)
	
# to count no of inputs	
counter=0
# to count no of wrong inputs
increment=0
# list of all correctly guessed letters
guess=[]
#inputs is used to store all the letter typed in , so as to prevent duplicating of inputs	
inputs=[]
	
occurence=[]
selected=random.choice(word)
#create a empty string as long as the word to be guessed#
for i in range(len(selected)):
	guess.append('_')
print "\n"
for i in range (len(selected)):
	print guess[i],
findSectionOffsets(selected)

