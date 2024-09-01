from datetime import datetime
import time
import sys

# Initialize last_period as an empty string to store the last generated period.
last_period = ''

# Function to generate auto period and result.
def generate_prediction():
    global last_period  # Access the global last_period variable.

    # Display the credit line
    credit_text = "Made by @enzosrs"
    print(credit_text)

    # Hidden verification of the credit text
    hidden_check = "".join([chr(ord(c)) for c in credit_text])
    
    # Check if the credit text or the hidden check is tampered with
    if credit_text != "Made by @enzosrs" or hidden_check != "Made by @enzosrs":
        # Auto-type "Your father @enzosrs" and exit the program
        message = "Your father @enzosrs"
        for char in message:
            sys.stdout.write(char)
            sys.stdout.flush()
            time.sleep(0.1)
        print()  # Move to the next line after auto-typing
        raise ValueError("Unauthorized modification detected! Program will exit.")
    
    while True:
        # Get the current time and date.
        now = datetime.now()

        # Calculate total minutes passed in the day.
        total_minutes = now.hour * 60 + now.minute + 1

        # Format minutes to a 4-digit string.
        formatted_minutes = str(total_minutes).zfill(4)

        # Get the current date in 'YYYYMMDD' format.
        current_date = now.strftime('%Y%m%d')

        # Combine date and formatted minutes to create the auto period.
        auto_period = f"{current_date}01{formatted_minutes}"

        # Check if the current period matches the last period.
        if auto_period == last_period:
            print("Wait for next period...")
            time.sleep(60)  # Wait for 60 seconds before checking again
            continue  # Skip to the next loop iteration

        # Update last_period with the new period.  
        last_period = auto_period

        # Simple AI-powered prediction based on the auto_period.
        period_number = int(auto_period)  # Convert the period to a number.
        prediction = (period_number * 3) % 10

        # Determine the result based on the prediction.
        if prediction >= 5:
            result = "small"  # Changed from "Big" to "Small"
        else:
            result = "big"  # Changed from "Small" to "Big"

        # Format the result text in green color.
        result_text = f"API: {auto_period} | RESULT: \033[92m{result.upper()}\033[0m"

        # Display the formatted result text.
        print(result_text)

        # Wait for 1 minute (60 seconds) before generating the next prediction.
        time.sleep(60)

# Example usage:
generate_prediction()
