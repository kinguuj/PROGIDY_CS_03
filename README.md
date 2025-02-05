# PROGIDY_CS_03
import re  # Importing the regular expressions module

def check_password_strength(password):
    """
    Assess the strength of a password based on criteria such as length,
    presence of uppercase and lowercase letters, numbers, and special characters.
    """
    # Initialize criteria flags
    length_flag = len(password) >= 8
    uppercase_flag = bool(re.search(r'[A-Z]', password))
    lowercase_flag = bool(re.search(r'[a-z]', password))
    number_flag = bool(re.search(r'[0-9]', password))
    special_char_flag = bool(re.search(r'[!@#$%^&*(),.?":{}|<>]', password))

    # Display feedback based on missing criteria
    feedback = []
    if not length_flag:
        feedback.append("Password must be at least 8 characters long.")
    if not uppercase_flag:
        feedback.append("Password must contain at least one uppercase letter.")
    if not lowercase_flag:
        feedback.append("Password must contain at least one lowercase letter.")
    if not number_flag:
        feedback.append("Password must contain at least one number.")
    if not special_char_flag:
        feedback.append("Password must contain at least one special character.")

    # Determine overall strength
    if all([length_flag, uppercase_flag, lowercase_flag, number_flag, special_char_flag]):
        return "Strong Password! ✅", feedback
    elif length_flag and sum([uppercase_flag, lowercase_flag, number_flag, special_char_flag]) >= 3:
        return "Moderate Password! ⚠️", feedback
    else:
        return "Weak Password! ❌", feedback


# Step 4: User input
password = input("Enter a password to check its strength: ")
strength_message, feedback_messages = check_password_strength(password)

# Show results
print(f"\nPassword Strength: {strength_message}")
if feedback_messages:
    print("\nSuggestions to improve your password:")
    for message in feedback_messages:
        print(f"- {message}")
