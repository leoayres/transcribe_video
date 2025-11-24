

# 📄 **README — Video Audio Extractor & Speech-to-Text Transcriber**

This project provides a simple and effective way to **extract audio from a video file** and **automatically transcribe speech into text**, using:

* **MoviePy** for audio extraction
* **SpeechRecognition** with Google’s free speech-to-text API
* **pydub** (optional) for audio manipulation

It is ideal for quickly generating transcripts from videos, analyzing spoken content, or converting video speech into text files.

---

## 🚀 **Features**

* 🎬 Extracts audio from video files (`.mp4`, `.avi`, etc.)
* 🎧 Converts the audio to `.wav`
* 🧠 Transcribes speech using **Google Speech Recognition**
* 📝 Automatically saves transcription to a `.txt` file
* 🔎 Includes error handling and informative messages
* 🗂 Simple, clean project structure

---

## 📦 **Installation**

Install the required libraries:

```bash
pip install moviepy SpeechRecognition pydub
```

---

## 📁 **Project Structure**

```
/your_project
│── video1.mp4
│── audio1.wav
│── transcription1.txt
│── main.py
```

---

## ▶️ **How to Use**

1. Place the input video in the project folder and name it `video1.mp4`
   *(or change the filename in the script)*

2. Run the script:

```bash
python main.py
```

3. The script will:

* Extract the audio → `audio1.wav`
* Transcribe speech to text
* Save the result → `transcription1.txt`

---

## 🧩 **Main Script**

```python
import moviepy.editor as mp
import speech_recognition as sr
import os

def extract_audio_from_video(video_path, audio_path):
    video = mp.VideoFileClip(video_path)
    video.audio.write_audiofile(audio_path)

def transcribe_audio_to_text(audio_path, text_output_path):
    recognizer = sr.Recognizer()
    
    with sr.AudioFile(audio_path) as source:
        audio = recognizer.record(source)
        
        try:
            text = recognizer.recognize_google(audio, language="pt-BR")
            print("Transcription: " + text)
            
            with open(text_output_path, 'w', encoding='utf-8') as file:
                file.write(text)
                
        except sr.UnknownValueError:
            print("Google Speech Recognition could not understand the audio")
        except sr.RequestError as e:
            print("Error requesting results from Google Speech Recognition; {0}".format(e))

def main():
    script_dir = os.path.dirname(os.path.abspath(__file__))
    video_path = os.path.join(script_dir, 'video1.mp4')
    audio_path = os.path.join(script_dir, 'audio1.wav')
    text_output_path = os.path.join(script_dir, 'transcription1.txt')

    extract_audio_from_video(video_path, audio_path)
    transcribe_audio_to_text(audio_path, text_output_path)

if __name__ == "__main__":
    main()
```

---

## 🌍 **Supported Languages**

You can change the transcription language by modifying:

```python
recognizer.recognize_google(audio, language="en-US")
```

---

## ⚠️ **Limitations**

* Requires an internet connection (Google Speech Recognition).
* Accuracy may decrease in noisy audio.
* Very long videos may require splitting into segments.

---

## 🛠 Future Improvements

* Support for **Whisper (OpenAI)** for high-accuracy offline transcription
* Automatic generation of `.srt` subtitle files
* Batch transcription for multiple videos
* Web interface (Flask / FastAPI)

---


