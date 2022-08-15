import json
import sys
import os
import time
import requests

_version = "^1.0.0"

def start(b):
    # update system
    response = requests.get("https://mdxwarriorxop.github.io/bread/update.html")
    data = json.loads(response.content.decode("UTF-8"))
    latestVersion = data["version"]
    
    if latestVersion != _version:
        # theres an update
        with open("newBread.py", "w") as nf:
            code = requests.get("https://mdxwarriorxop.github.io/bread/bread.txt")
            nf.write(str(code.content))
            
        os.rename("bread.py", "oldBread.py")
        os.rename("newBread.py", "bread.py")
        os.system(f"python {os.getcwd()}/bread.py")
            
    
    # start game
    if not(b):      
        timeToSleep = 1
        print("Welcome to the BREAD")
        time.sleep(timeToSleep)
        print("as we all know, Bread is awesome, very cool and tasty")
        time.sleep(timeToSleep)
        print("So i decided to create a game about it!")
        time.sleep(timeToSleep)
        mode = input("So what do you want to do today? (eat/bake)> ")
        startGame(mode)
    else:
        mode = input("So what do you want to do today? (eat/bake)> ")
        startGame(mode)
        

def startGame(mode):
    if mode == "eat":
        # you wanna eat bread
        while(True):
            type = input("Which Bread Would You Like To Eat?\n(q to quit, p to go to previous section)>\n").lower()
            if type == "q" or type == "quit":
                sys.exit()
            if type == "p" or type == "previous":
                start(True)
                
            eat(type)
            
    elif mode == "bake":
        # you wanna bake some bread
        while(True):
            type = input("Which Bread Would You Like To Bake?\n(q to quit, p to go to previous section)>\n").lower()
            
            if type == "q" or type == "quit":
                sys.exit()
            if type == "p" or type == "previous":
                start(True)
                
            bake(type)
    else:
        print("Invalid Mode!")
        return sys.exit()
    

def eat(type):
    aOrAn = aOrAnFinder(type)
            
    print(f"You ate {aOrAn} {type}")
    return None

def bake(type):
    aOrAn = aOrAnFinder(type)
            
    print(f"You baked {aOrAn} {type}")

def aOrAnFinder(type):
    if type.startswith("a") or type.startswith("e") or type.startswith("i") or  type.startswith("o") or type.startswith("u"):
            aOrAn = "an"
    else:
            aOrAn = "a"
            
    return aOrAn

if __name__=="__main__":
    start(False)
