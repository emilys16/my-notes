---
title: ★ The Great Golden Adventure - Python Exercise 1
draft: false
tags:
  - CTS2000
---
 ___
#### Design Influence
We tested the text game *The Oregon Trail*. It influenced our own design by using an adventure type theme.

#### Game Premise and Creation Process
The premise of our game is to go on a hunt using your late grandfathers old treasure map to find hidden gold. During the creation process we encountered challenges in defining the functions. Each newly defined function needed to be put in a certain order for the code to run properly. In the future we would like to add more branches to the story and try to make the defined functions more concise. 


```python
# Import a python library called time
import time

# ... DEFINING NEW FUNCTIONS ......................
def game_over(message): # "You lose" function that ends the game
    print(" ")
    print(message)
    print("Game Over. You Lose.")
    time.sleep(2)  # brief pause before exiting
    quit() #end game

def boat(): # (A) of choice 1
    time.sleep(2)
    print(" ")
    print("You come aboard the boat and navigate the rising tides and crashing waves until the storm is too much to bear.")
    print("You notice a small island in the distance but worry that the tides are too strong and will push you off-course.")
    print(" ")
    time.sleep(2)
    return
    
def helicopter(): # (B) of choice 1
    time.sleep(3)
    print(" ")
    print("You get on the helicopter and fly towards the treasure.")
    print("As you fly, the winds grow more and more dangerous.")
    time.sleep(2)
    print(" ")
    print("On your radar, you notice a small chunk of land.")
    print("'It may just be debris from the storm messing up the signals,' you think to yourself.")
    time.sleep(3)
    print(" ")
    print("The storm is getting worse and you have to act now.")
    print(" ")
    return

def anchor_boat(): # (A) of choice 2.1
    time.sleep(3)
    print(" ")
    print("You drop anchor and wait for the storm to pass.")
    print("The waves tear through the sides of your boat. The hull fills with water and the ocean devours you.")
    print("...")
    time.sleep(1)
    game_over("Cause of death: Drowning.")
    return

def sail_island(): # (B) of choice 2.1
    time.sleep(3)
    print(" ")
    print("You sail towards the island and hope for safety.")
    print("The waves grow rough and mean. You hear the howling of the wind and the waves rock the boat until you can barely stand...")
    time.sleep(1)
    print("...")
    print("Luckily, the tide continues to push you closer to the island's shore.")
    time.sleep(1)
    print("...")
    time.sleep(1)
    print("Finally, you crash into the sandy beach as the skies clear and the rain subsides.")
    print("You did it! You landed on the island!")
    print(" ")
    time.sleep(3)
    print("You look around and see a small village. The people seem friendly, but they could just slow you down...")
    print(" ")
    time.sleep(1)
    return  

def land_helicopter(): # (A) of choice 2.2
    time.sleep(3)
    print(" ")
    print("As the winds become more powerful, you struggle to control the aircraft.")
    print("You feel the controls loosen. You think to yourself,'This is it.'")
    print("Finally, you notice the small island below you. You decrease your altitude before disengaging the engines.")
    time.sleep(1)
    print("...")
    print("As you free-fall out of the sky, your stomach drops.")
    time.sleep(1)
    print("...")
    time.sleep(1)
    print("*THUD*")
    print("You did it! You landed on the island!")
    print(" ")
    time.sleep(3)
    print("You look around and see a small village. The people seem friendly, but they could just slow you down...")
    print(" ")
    time.sleep(1)
    return
    
def fly_helicopter(): # (B) of choice 2.2
    time.sleep(3)
    print(" ")
    print("As you fly, the winds continue to grow until the metal panels of your helicopter can't take it anymore.")
    time.sleep(1)
    print(" ")
    print("Alarms start to go off and red lights flash as you lose control of the aircraft.")
    print("You crash into the cold ocean water and disappear beneath the waves.")
    print("...")
    time.sleep(1)
    game_over("Cause of death: Drowning.")
    return

def ask_help(): # (A) of choice 3
    time.sleep(3)
    print(" ")
    print("You go into the local village to find help. A woman named Theresa says she is familiar with the land and will help you find the cave on your map!")
    time.sleep(2)
    print("She leads you to a winding path in a secluded area of the island.")
    time.sleep(2)
    print(" ")
    print("...")
    print(" ")
    time.sleep(2)
    print("'I hope she *actually* knows where she's going,' you think to yourself.")
    time.sleep(2)
    print(" ")
    print("...")
    print(" ")
    time.sleep(2)
    print("'Here we are!' says Theresa, gleefully.")
    print("You successfully reached the cave to find your grandfathers hidden treasure!")
    print(" ")
    print("Standing outside the cave, you realize you don't have anything to offer Theresa for her service, and you start to feel a bit badly...")
    print(" ")
    return
    
def go_alone(): # (B) of choice 3
    time.sleep(3)
    print(" ")
    print("As you naviagte the dense jungle, you start to lose your bearings and forget which way you came from.")
    time.sleep(1)
    print("...")
    time.sleep(1)
    print("*SNAP!*")
    time.sleep(1)
    print("A jaguar jumps out infront of you!")
    print("You try to run but its too fast. It grabs you with its claws and tears you limb from limb")
    print("...")
    time.sleep(1)
    game_over("Cause of death: Shredded to pieces by jaguar.")
    return

def cave_join(): # (A) of choice 4
    time.sleep(4)
    print(" ")
    print("You go down twists and turns in the cave until you enter a cavern. The cavern is filled with gold and jewels.")
    time.sleep(2)
    print(" ")
    print("An eerie feeling overwhelms you.")
    time.sleep(2)
    print(" ")
    print("Your accomplice, Theresa, is overcome with greed. She decides she wants all of the treasure for herself.")
    print("...")
    time.sleep(1)
    print("Suddenly, you see a shadow reaching above your head and towering over you.")
    print(" ")
    time.sleep(1)
    print("...")
    game_over("Cause of death: Stab wound & loss of blood.")
    return

def cave_alone(): # (B) of choice 4
    time.sleep(3)
    print(" ")
    print("You go down twists and turns in the cave until you enter a cavern. The cavern is filled with gold and jewels.")
    print("Congratualtions! You were successful in finding your grandfathers treasure!")
    return 
    
# ... END OF DEFINING NEW FUNCTIONS ....................

# ... START OF THE GAME CHOICES.........................
name = input("Enter your name: ")
print("Hello,", name, "the traveller!")
print("You are on a quest for forgotten gold after finding your great grandfathers old treasure map!")


# Choice 1: Get on a boat or helicopter
time.sleep(3)
print(" ")
print("You are standing on the coast of your local beach. The day is gloomy and it seems like there may be a storm coming in.")
print("That doesn't stop you from going on the adventure of a lifetime. You are anything but afraid.")
print("As you look to your right, you see a boat. When you look to your left, you see a helicopter.")
time.sleep(6)
print(" ")
print("You have two options:")
print("A) Get on a boat to find the treasure.")
print("B) Get on a helicopter to find the treasure.")

while True:
    choice1 = input("What do you do? (A/B): ") #pick mode of transportation (boat or helicopter)

    #Choice 2.1 BOAT option: anchor the boat or sail through the storm
    if choice1.upper() == "A":
        boat()
        print("You have two options:")
        print("A) Anchor the boat and wait until the storm passes to go to the island.")
        print("B) Sail towards the island and hope for safety.")
        while True:
            choice2 = input("What do you do? (A/B): ")
            if choice2.upper() == "A":
                anchor_boat()
                break
            elif choice2.upper() == "B":
                sail_island()
                break
            else:
                print("Invalid choice. Please enter A or B.")

    # Choice 2.2 HELICOPTER option: Emergency landing or fly through the storm
    elif choice1.upper() == "B":
        helicopter()
        print("You have two options:")
        print("A) Continue flying until you are certain you've found land.")
        print("B) Risk making an emergency landing.")
        while True:
            choice2 = input("What do you do? (A/B): ")
            if choice2.upper() == "A":
                fly_helicopter()
                break
            elif choice2.upper() == "B":
                land_helicopter()
            else:
                print("Invalid choice. Please enter A or B.")
        break
        
    else: #linking the ELSE statement back up to choice 1 in case user inputs an invalid choice
        print("Invalid choice. Please enter A or B.")

# Choice 3: ask a local for help or navigate alone but only if player survived thus far - indicated by choice notation
    if choice2.upper() == "B":
        print("You have two options:")
        print("A) Ask a local for help.")
        print("B) Go alone and navigate yourself.")
        choice3 = input("What do you do? (A/B): ")
        if choice3.upper() == "A":
            ask_help()
        elif choice3.upper() == "B":
            go_alone()
        else:
            print("Invalid choice. Please enter A or B.")

# Choice 4: find the treasure with Theresa or find it alone
    if choice3.upper() == "A":
        print("You have two options:")
        print("A) Ask Theresa to join you in the treasure hunt.")
        print("B) Thank Theresa for her help and go inside the cave alone.")    
        choice4 = input("What do you do? (A/B): ")    
        if choice4.upper() == "A":
            cave_join()
            break
        elif choice4.upper() == "B":
            cave_alone()
            break
        else:
            print("Invalid choice. Please enter A or B.")
            break 
    else: 
        print("Invalid choice. Please enter A or B.")
        break
```
