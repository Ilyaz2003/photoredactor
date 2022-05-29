import PySimpleGUI as sg
import os
import io
from PIL import Image, ImageDraw, ImageTk, ImageFont
import base64
import subprocess
import sys

orange64 = 255, 215, 0
green_pill64 = 0, 128, 0
red_pill64 = 255, 0, 0
button64 = 255, 255, 224


def image_file_to_bytes(image64, size):
    image_file = io.BytesIO(base64.b64decode(image64))
    img = Image.open(image_file)
    img.thumbnail(size, Image.ANTIALIAS)
    bio = io.BytesIO()
    img.save(bio, format='PNG')
    imgbytes = bio.getvalue()
    return imgbytes


def ShowMeTheButtons():
    bcolor = ('black', 'black')
    wcolor = ('white', 'black')

    sg.theme('Black')
    sg.set_options(auto_size_buttons=True, border_width=0,
                   button_color=sg.COLOR_SYSTEM_DEFAULT)

    toolbar_buttons = [[sg.Text('Who says Windows have to be ugly when using tkinter?', size=(45, 3))],
                       [sg.Text(
                           'All of these buttons are part of the code itself', size=(45, 2))],
                       [sg.RButton('Next', image_data=image_file_to_bytes(button64, (100, 50)), button_color=wcolor, font='Any 15', pad=(0, 0), key='-close-'),
                        # [sg.RButton('Exit', image_data=image_file_to_bytes(black64, (100,50)),button_color=bcolor, font='Any 15', pad=(0,0), key='-close-'),],
                        sg.RButton('Submit',
                                   image_data=image_file_to_bytes(
                                       red_pill64, (100, 50)),
                                   button_color=wcolor, font='Any 15', pad=(0, 0), key='-close-'),
                        sg.RButton('OK', image_data=image_file_to_bytes(green_pill64, (100, 50)),
                                   button_color=bcolor, font='Any 15', pad=(0, 0), key='-close-'),
                        sg.RButton('Exit', image_data=image_file_to_bytes(orange64, (100, 50)), button_color=bcolor, font='Any 15', pad=(0, 0), key='-close-'), ],
                       ]


    layout = [[sg.Frame('Nice Buttons', toolbar_buttons,
                        font=('any 18'), background_color='black')]]

    window = sg.Window('Demo of Nice Looking Buttons', layout,
                       no_titlebar=False, grab_anywhere=True,
                       keep_on_top=True, use_default_focus=False,
                       font='any 15', background_color='black', finalize=True)


    while True:
        button, value = window.read()
        print(button)
        if button == '-close-' or button is None:
            break           # exit button clicked


if __name__ == '__main__':

    ShowMeTheButtons()
