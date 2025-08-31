import tkinter as tk
import time
import random

# Sample sentences for typing
sentences = [
    "CodeClause provides amazing internship opportunities.",
    "Python is a very powerful programming language.",
    "Typing fast and accurately is a useful skill.",
    "Artificial Intelligence is shaping the future.",
    "Practice makes a person perfect in programming."
]

class TypingSpeedTest:
    def __init__(self, root):
        self.root = root
        self.root.title("Typing Speed Calculator")
        self.root.geometry("700x400")
        self.start_time = None
        self.sentence = random.choice(sentences)

        self.label = tk.Label(root, text="Type the sentence below:", font=("Arial", 14))
        self.label.pack(pady=10)

        self.sentence_label = tk.Label(root, text=self.sentence, font=("Arial", 16), wraplength=600, justify="center")
        self.sentence_label.pack(pady=10)

        self.text_entry = tk.Entry(root, width=70, font=("Arial", 14))
        self.text_entry.pack(pady=10)
        self.text_entry.bind("<FocusIn>", self.start_typing)

        self.submit_button = tk.Button(root, text="Submit", command=self.calculate_speed, font=("Arial", 12))
        self.submit_button.pack(pady=10)

        self.result_label = tk.Label(root, text="", font=("Arial", 14))
        self.result_label.pack(pady=10)

    def start_typing(self, event):
        if self.start_time is None:
            self.start_time = time.time()

    def calculate_speed(self):
        end_time = time.time()
        typed_text = self.text_entry.get()

        # Calculate typing speed
        time_taken = end_time - self.start_time
        words = typed_text.split()
        num_words = len(words)
        wpm = (num_words / time_taken) * 60

        # Calculate accuracy
        correct_words = sum(1 for i, word in enumerate(typed_text.split()) if i < len(self.sentence.split()) and word == self.sentence.split()[i])
        accuracy = (correct_words / len(self.sentence.split())) * 100

        self.result_label.config(text=f"Speed: {wpm:.2f} WPM | Accuracy: {accuracy:.2f}%")

# Run app
root = tk.Tk()
app = TypingSpeedTest(root)
root.mainloop()
