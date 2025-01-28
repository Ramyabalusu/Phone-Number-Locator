import phonenumbers
from phonenumbers import geocoder, carrier

def locate_phone_number(phone_number):
    try:
        # Parse the phone number
        parsed_number = phonenumbers.parse(phone_number, "CH")
        
        # Get the geographical location
        location = geocoder.description_for_number(parsed_number, "en")
        
        # Get the carrier information
        service_provider = carrier.name_for_number(parsed_number, "en")
        
        return location, service_provider
    except phonenumbers.NumberParseException as e:
        return str(e), None

def main():
    phone_number = input("Enter the phone number (with country code, e.g., +14155552671): ")
    
    location, service_provider = locate_phone_number(phone_number)
    
    if service_provider:
        print(f"Location: {location}")
        print(f"Service Provider: {service_provider}")
    else:
        print(f"Error: {location}")

if _name_ == "_main_":
    main()
