# python-xmis-kodi
xmis kodi
import speech_recognition as sr
import os
import sys
import webbrowser
import pyttsx3

def talk(words):
    engine = pyttsx3.init()
    engine.say(words)
    engine.runAndWait()

talk("heloo, talk me")

def command():
    r = sr.Recognizer()

    with sr.Microphone() as source:
        print("talk")
        r.pause_threshold = 1
        r.adjust_for_ambient_noise(source, duration=1)
        audio = r.listen(source)

    try:
        zadanie = r.recognize_google(audio).lower()
        print("you talk:" + zadanie)
    except sr.UnknownValueError:
        talk("i am not undersand")
        zadanie = command()
    return  zadanie

def makeSomething(zadanie):
    if 'open website' in zadanie:
        talk ("yje otkrivaiu")
        url = 'https://itproger.com'
        webbrowser.open(url)
    elif 'stop' in zadanie:
        talk ("da , kanechna, bez , problem")
        sys.exit()

while True:
    makeSomething( command())
