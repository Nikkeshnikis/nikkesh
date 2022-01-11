
import pyttsx3
import datetime
import subprocess

def speak(audio):
    engine.say(audio)
    engine.runAndWait()

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty("voices",voices[1].id)

def wishme():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning!")

    elif hour>=12 and hour<14:
        speak("Good Afternoon!")

    elif hour>=14 and hour<18:
        speak("Good Evening!")

    else:
        speak("Good Night!")
    print("I am JARVIS Sir. Please tell me how may I help you")
    speak("I am JARVIS Sir. Please tell me how may I help you")  
wishme()

def time():
    engine.setProperty("rate",130)
    strTime = datetime.datetime.now().strftime("%I:%M %p")    #("%H:%M:%S")  
    speak(f"Sir,the time is {strTime}")
   
def date():
   
    strday = datetime.datetime.now().day
    #print(f"Sir, the DAY is {strday}")
    strmonth = datetime.datetime.now().month
    #print(f"Sir, the MONTH is {strmonth}")
    stryear = datetime.datetime.now().year
    #print(f"Sir, the YEAR is {stryear}")
    engine.setProperty("rate",130)
    date=f"{strday} :{strmonth} :{stryear}"
    speak("TODAY DATE is "+date)
   
def day():
    strday = datetime.datetime.now().day
    strmonth = datetime.datetime.now().month
    stryear = datetime.datetime.now().year
    date=str(f"{strday} {strmonth} {stryear}")
    day_name=['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday']
    day= datetime.datetime.strptime(date,'%d %m %Y').weekday ()
    speak("TODAY is "+day_name[day])

def ip():
    try:
        lan_ip = (socket.gethostbyname(socket.gethostname()))
        engine.setProperty("rate",130)
        speak("YOUR LOCAL IP ADDRESS is"+lan_ip)
       
    except:
        speak("IP ADDRESS NOT FOUND")

def shut():
    speak("Please Confirm Sir   ")
    confirm=input("CONFIRM : ")
    if "yes" in confirm:
        speak("Shutdowning System in 3 Seconds 3, 2, 1 ")
        subprocess.call(['shutdown','/p'])
    else:
        speak("Termenating SHUTDOWN PROTOCAL")


def main():
    while True:
        fri=input("JARVIS >>> ")
        fri=fri.lower()
        if "ip" in fri:
            ip()
        if "time" in fri:
            time()
        if "date" in fri:
            date()
        if "day" in fri:
            day()
        if "shutdown" in fri:
            shut()
        if "bye" in fri:
            exit()

main
