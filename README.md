# auto-reply-bot
this bot helps you to reply automatically based on your last chats 

#  auto reply bot
import pyautogui
import pyperclip
import time
from openai import OpenAI


client=OpenAI( 
  api_key="API_KEY"
  )


def lastmessagefrombhargav(chat_log,sender_name="Bhargav"):
#   split the chat log into singl mssg
  messages=chat_log.strip().split("/2024")[-1]
  if sender_name in messages:
    return True
  return False

# click to get entered into chrome page
pyautogui.click(1317,1173)
time.sleep(1)


while True:
  time.sleep(3)
#   seletion of drag location from nd to 
  pyautogui.moveTo(597,214)
  pyautogui.dragTo( 1822,1107, duration=0.5,button='left')

#   copy the content to the clipboard
  pyautogui.hotkey('ctrl','c')
  time.sleep(2)
  pyautogui.click(629,827)
  
#   unselect the selected chats
  pyautogui.click(1108,513)
#   exit from chrome
  pyautogui.click(1778,25)
  time.sleep(5)


#   reopen the chrome page

  pyautogui.click(1317,1173)
  time.sleep(1)



#    retrive the data from clipboard and paste in the variable
  chat_history=pyperclip.paste()
  print(chat_history)

  print(lastmessagefrombhargav(chat_history))

  if lastmessagefrombhargav(chat_history):
    completion = client.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role":"sysytem" ,"content":"you are a person named anshul who speaks hindias well as english . you are from india and you are a codeer from shimla near mall road . you analyze chat history and respond like anshul . output should be the next chat respoinse as anshul . output should be next chat response { text message only} "},
        {"role":"system","content":"do not start  like this [21:02,12/6/2024] Bhargav"},
        {"role":"user","content":chat_history}
         ]
         )
    
    response=completion.choice[0].message.content
    pyperclip.copy(response)

# Click at coordinates (811, 1100)
    pyautogui.click(811, 1100)
    time.sleep(1)
#  paste the response in the type box 
    pyautogui.hotkey('ctrl','v')
    time.sleep(1)

# Press Enter
    pyautogui.press("enter")

