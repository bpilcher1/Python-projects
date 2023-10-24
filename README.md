# Python-projects
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.application import MIMEApplication

# Email configuration
sender_email = 'your_email@gmail.com'
receiver_email = 'recipient_email@gmail.com'
password = 'your_password'
subject = 'Test Email'
message = 'This is a test email sent from Python.'

# Create the email message
msg = MIMEMultipart()
msg['From'] = sender_email
msg['To'] = receiver_email
msg['Subject'] = subject

# Attach the message to the email
msg.attach(MIMEText(message, 'plain'))

# You can attach files like this:
# file_path = 'path_to_attachment.txt'
# with open(file_path, 'rb') as attachment:
#     part = MIMEApplication(attachment.read(), Name='attachment.txt')
# part['Content-Disposition'] = f'attachment; filename={file_path}'
# msg.attach(part)

# Connect to the SMTP server and send the email
try:
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.starttls()
    server.login(sender_email, password)
    server.sendmail(sender_email, receiver_email, msg.as_string())
    server.quit()
    print("Email sent successfully")
except Exception as e:
    print(f"An error occurred: {str(e)}")
