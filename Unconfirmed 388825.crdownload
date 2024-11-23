import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import sys  

# Initialize the text-to-speech engine
engine = pyttsx3.init()

# Set properties for the voice assistant
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)  # You can change [0] to [1] for a female voice
engine.setProperty('rate', 150)  # Adjust speaking speed

def speak(text):
    """Convert text to speech."""
    engine.say(text)
    engine.runAndWait()

def greet_user():
    """Greet the user based on the time of day."""
    hour = datetime.datetime.now().hour
    if 0 <= hour < 12:
        speak("Good Morning!")
    elif 12 <= hour < 18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")
    speak("I am your assistant. How can I help you today?")

def take_command():
    """Listen to the user's command and return it as text."""
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)
        try:
            audio = recognizer.listen(source, timeout=5, phrase_time_limit=5)
            print("Recognizing...")
            query = recognizer.recognize_google(audio, language='en-in')
            print(f"You said: {query}")
            return query.lower()
        except sr.UnknownValueError:
            speak("Sorry, I didn't catch that. Could you please repeat?")
            return None
        except sr.RequestError:
            speak("I am unable to connect to the speech recognition service.")
            return None

def perform_task(query):
    """Perform tasks based on the user's command."""
    if 'open google' in query:
        speak("Opening Google")
        webbrowser.open("https://www.google.com")
    elif 'open youtube' in query:
        speak("Opening Youtube")
        webbrowser.open("https://www.youtube.com")
    elif 'time' in query:
        current_time = datetime.datetime.now().strftime("%I:%M %p")
        speak(f"The time is {current_time}")
    elif 'exit' in query or 'stop' in query:
        speak("Goodbye! Have a nice day!")
        sys.exit()  # Exit the program using sys.exit()
    else:
        speak("Sorry, I don't know how to do that yet.")

# Main program
if __name__ == "__main__":
    greet_user()
    while True:
        command = take_command()
        if command:
            perform_task(command)
