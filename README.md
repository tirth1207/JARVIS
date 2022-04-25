import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes
import webbrowser
import smtplib

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)


def talk(text):
    engine.say(text)
    engine.runAndWait()


def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'tony' in command:
                command = command.replace('tony', '')
                print(command)
    except:
        pass
    return command


      
    
    
def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        talk("Good Morning!")
        print("Good Morning...")

    elif hour>=12 and hour<16:
        talk("Good Afternoon!")   
        print("Good Afternoon!")

    elif hour>=16 and hour<19:
        talk("Good Evening!")
        print("Good Evening!")
    else:
        talk("Good Night!")  
        print("Good Night!")

    talk("I am Jarvis Sir. Please tell me how may I help you") 
    print("I am Jarvis Sir. Please tell me how may I help you")
    
def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('rathod2304hetal@gmail.com', 'tirth1207')
    server.sendmail('alpeshrathod78@gmail.com', to, content)
    server.close()
    
    
def run_tony():
    command = take_command()
    print(command)
    if 'play' in command:
        print('Recognizing...')
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        print('Recognizing...')
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
        print("time is "+ time)
    elif 'wikipedia' in command:
        print('Recognizing...')
        person = command.replace('wikipedia', '')
        info = wikipedia.summary(person, 5)
        print(info)
        talk(info)
    elif 'date' in command:
        print('Recognizing...')
        date = datetime.datetime.now().strftime('%b: %d %y')
        talk('today is ' + date)
        print('today is ' + date)
    elif 'are you single' in command:
        print('Recognizing...')
        talk('I am in a relationship with wifi')
    elif 'joke' in command:
        print('Recognizing...')
        print(pyjokes.get_joke())
        talk(pyjokes.get_joke())
    elif 'google' in command:
        print('Recognizing...')
        webbrowser.open("google.com")
        talk('opening google')
    elif 'youtube' in command:
        print('Recognizing...')
        webbrowser.open("youtube.com")
        talk('opening youtube')
    elif 'who are you' in command:
        talk('i am jarvis. version 1.3.0. how can i help you?')
    elif 'how are you' in command:
        talk('i am fine. how are you sir?')
    elif 'i am fine' in command:
        talk('i  happy  to  know, that you are happy sir')
    elif 'send email ' in command:
            try:
                talk("What should I say?")
                content = take_command()
                to = "alpeshrathod78@gmail.com"    
                sendEmail(to, content)
                talk("Email has been sent!")
            except Exception as e:
                talk("Sorry sir. I am not able to send this email")        
    else:
        talk('Please say the command again.')            
if __name__ == "__main__":
    wishMe()

         
        
while True:
    run_tony()
