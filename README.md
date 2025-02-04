# Organized-files

import os
import shutil

def organize_files(directory):
    if not os.path.exists(directory):
        print("Directory not found!")
        return
        
#dec. type file

    file_types = {
        "Images": [".jpg", ".jpeg", ".png", ".gif"],
        "Documents": [".pdf", ".docx", ".txt"],
        "Videos": [".mp4", ".mkv"],
        "Music": [".mp3", ".wav"],
        "Others": []
    }

    for file in os.listdir(directory):
        file_path = os.path.join(directory, file)
        if os.path.isfile(file_path):
            file_ext = os.path.splitext(file)[1]
            folder_name = "Others"

            for category, extensions in file_types.items():
                if file_ext in extensions:
                    folder_name = category
                    break

            folder_path = os.path.join(directory, folder_name)
            os.makedirs(folder_path, exist_ok=True)
            shutil.move(file_path, os.path.join(folder_path, file))
            print(f"Moved {file} to {folder_name}")

if __name__ == "__main__":
    directory = input("Enter the path of the folder to organize way: ")
    organize_files(directory)
