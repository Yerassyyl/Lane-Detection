import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import numpy as np
import os
import random
from PIL import Image

def get_random_image_path(folder_path):
    """
    Get the path to a random image within the specified folder.
    """
    # Get a list of all image files in the folder
    image_files = [file for file in os.listdir(folder_path) if file.lower().endswith('.jpg')]

    if not image_files:
        print(f"No image files found in the specified folder: {folder_path}")
        return None

    # Take a random image file
    random_image = random.choice(image_files)

    # Construct the full path for the random image
    random_image_path = os.path.join(folder_path, random_image)

    return random_image_path

if __name__ == "__main__":
    # Specify the folder path containing images
    #ПОМЕНЯТЬ ПУТЬ К ПАПКЕ, ГДЕ ЛЕЖАТ ТЕСТОВЫЕ ИЗОБРАЖЕНИЯ!
    folder_path = "C:\\Users\\Ard\\Desktop\\Lane_detection\\test_images"

    # Call the function to get the path of a random image from the folder
    random_image_path = get_random_image_path(folder_path)

    if random_image_path:
        # Read and display the random image using matplotlib
        image = mpimg.imread(random_image_path)




# Grab the x and y size and make a copy of the image
ysize = image.shape[0]
xsize = image.shape[1]
color_select = np.copy(image)

# Define color selection criteria
###### MODIFY THESE VARIABLES TO MAKE YOUR COLOR SELECTION
red_threshold = 160
green_threshold = 160
blue_threshold = 160
######

rgb_threshold = [red_threshold, green_threshold, blue_threshold]

# Do a boolean or with the "|" character to identify
# pixels below the thresholds
thresholds = (image[:,:,0] < rgb_threshold[0]) \
            | (image[:,:,1] < rgb_threshold[1]) \
            | (image[:,:,2] < rgb_threshold[2])
color_select[thresholds] = [0,0,0]

# Display the image
plt.imshow(image)
plt.title("Input Image")
plt.show()
plt.imshow(color_select)
plt.title("Color Selected Image")
plt.show()
