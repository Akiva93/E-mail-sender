# E-mail-sendre
Create an e-mail sender with python that will not end up in a spam folder when you send a multiple e-mail
import tkinter as tk
import smtplib
import threading

def send_email():
    # Get the sender's email address and password.
    sender_email = email_entry.get()
    sender_password = password_entry.get()

    # Get the recipient's email addresses.
    recipient_emails = recipient_entry.get().split(",")

    # Get the subject and body of the email.
    subject = subject_entry.get()
    body = body_entry.get()

    # Create an SMTP object and connect to the email server.
    smtp = smtplib.SMTP("smtp.gmail.com", 587)
    smtp.starttls()
    smtp.login(sender_email, sender_password)

    # Create a thread to send the email to each recipient.
    for recipient_email in recipient_emails:
        thread = threading.Thread(target=send_email_thread, args=(smtp, recipient_email, subject, body))
        thread.start()

def send_email_thread(smtp, recipient_email, subject, body):
    # Send the email.
    smtp.sendmail(sender_email, recipient_email, f"Subject: {subject}\n\n{body}")

root = tk.Tk()

email_label = tk.Label(root, text="Sender's email address:")
email_entry = tk.Entry(root)

password_label = tk.Label(root, text="Sender's password:")
password_entry = tk.Entry(root, show="*")

recipient_label = tk.Label(root, text="Recipient's email addresses:")
recipient_entry = tk.Entry(root)

subject_label = tk.Label(root, text="Subject:")
subject_entry = tk.Entry(root)

body_label = tk.Label(root, text="Body:")
body_entry = tk.Text(root)

send_button = tk.Button(root, text="Send", command=send_email)

email_label.pack()
email_entry.pack()

password_label.pack()
password_entry.pack()

recipient_label.pack()
recipient_entry.pack()

subject_label.pack()
subject_entry.pack()

body_label.pack()
body_entry.pack()

send_button.pack()

root.mainloop()
