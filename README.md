- 👋 Hi, I’m @Hariomkrpintu
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Hariomkrpintu/Hariomkrpintu is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import streamlit as st
import cv2
import numpy as np

# Set black background
st.set_page_config(page_title="Tutor App", page_icon="🎓", layout="wide", initial_sidebar_state="collapsed", page_bg_color="#000000")

# Screen share
def screen_share():
  cap = cv2.VideoCapture(0)
  while True:
    ret, frame = cap.read()
    if ret:
      frame = cv2.resize(frame, (640, 480))
      st.image(frame, channels="BGR")
    else:
      break
  cap.release()

# Video upload
def video_upload():
  uploaded_file = st.file_uploader("Upload video")
  if uploaded_file is not None:
    video_bytes = uploaded_file.read()
    video = cv2.VideoCapture(video_bytes)
    while True:
      ret, frame = video.read()
      if ret:
        frame = cv2.resize(frame, (640, 480))
        st.image(frame, channels="BGR")
      else:
        break
    video.release()

# Image upload
def image_upload():
  uploaded_file = st.file_uploader("Upload image")
  if uploaded_file is not None:
    image_bytes = uploaded_file.read()
    image = cv2.imdecode(np.fromstring(image_bytes, np.uint8), cv2.IMREAD_COLOR)
    st.image(image, channels="BGR")

# Notice section
def notice_section():
  st.header("Notices")
  # Fetch notices from database and display them here

# Store section
def store_section():
  st.header("Store")
  # Display products from store here

# DPP section
def dpp_section():
  st.header("DPPs")
  # Display DPPs from database here

# Live class
def live_class():
  st.header("Live Class")
  # Start live class here

# Sidebar
st.sidebar.header("Menu")
st.sidebar.selectbox("Select section", ["Screen share", "Video upload", "Image upload", "Notice section", "Store section", "DPP section", "Live class"])

# Main section
if st.sidebar.selectbox("Select section") == "Screen share":
  screen_share()
elif st.sidebar.selectbox("Select section") == "Video upload":
  video_upload()
elif st.sidebar.selectbox("Select section") == "Image upload":
  image_upload()
elif st.sidebar.selectbox("Select section") == "Notice section":
  notice_section()
elif st.sidebar.selectbox("Select section") == "Store section":
  store_section()
elif st.sidebar.selectbox("Select section") == "DPP section":
  dpp_section()
elif st.sidebar.selectbox("Select section") == "Live class":
  live_class()
