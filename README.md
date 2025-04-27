# eco-factor

Creating a Python program to calculate and suggest ways to reduce carbon footprints involves several key components. Below is a basic implementation of the `eco-factor` tool, which calculates the carbon footprint from various everyday activities such as traveling, energy consumption, and waste generation. This program also provides recommendations for minimizing the carbon footprint based on user inputs. The program includes error handling and comments for clarity.

```python
# eco_factor.py

def calculate_transportation_footprint(mileage, fuel_efficiency, fuel_type):
    """Calculate carbon footprint for transportation."""
    CO2_PER_GALLON_GAS = 19.6  # lbs of CO2 per gallon for gasoline
    CO2_PER_GALLON_DIESEL = 22.4  # lbs of CO2 per gallon for diesel

    try:
        gallons_used = mileage / fuel_efficiency
        if fuel_type.lower() == "gasoline":
            return gallons_used * CO2_PER_GALLON_GAS
        elif fuel_type.lower() == "diesel":
            return gallons_used * CO2_PER_GALLON_DIESEL
        else:
            raise ValueError("Invalid fuel type")
    except ZeroDivisionError:
        print("Fuel efficiency cannot be zero.")
        return 0
    except Exception as e:
        print(f"Error calculating transportation footprint: {e}")
        return 0

def calculate_energy_footprint(kwh, energy_source):
    """Calculate carbon footprint for energy consumption."""
    CO2_PER_KWH_GRID = 0.92  # lbs of CO2 per kWh for grid electricity
    CO2_PER_KWH_RENEWABLE = 0.03  # lbs of CO2 per kWh for renewable sources

    try:
        if energy_source.lower() == "grid":
            return kwh * CO2_PER_KWH_GRID
        elif energy_source.lower() == "renewable":
            return kwh * CO2_PER_KWH_RENEWABLE
        else:
            raise ValueError("Invalid energy source")
    except Exception as e:
        print(f"Error calculating energy footprint: {e}")
        return 0

def calculate_waste_footprint(pounds, recycling_rate):
    """Calculate carbon footprint for waste generation."""
    CO2_PER_POUND_WASTE = 2.5  # lbs of CO2 per pound of waste

    try:
        unrecycled_waste = pounds * (1 - (recycling_rate / 100))
        return unrecycled_waste * CO2_PER_POUND_WASTE
    except Exception as e:
        print(f"Error calculating waste footprint: {e}")
        return 0

def give_recommendations(transportation_fp, energy_fp, waste_fp):
    """Provide recommendations to reduce carbon footprint."""
    print("\nRecommendations to reduce your carbon footprint:")
    if transportation_fp > 0:
        print("- Consider using public transportation, carpooling, or switching to an electric vehicle to reduce transportation emissions.")
    if energy_fp > 0:
        print("- Switching to renewable energy sources like solar panels or wind turbines can significantly reduce energy emissions.")
    if waste_fp > 0:
        print("- Improving your recycling habits and reducing waste can lower your waste-derived carbon footprint.")

def main():
    print("Welcome to Eco-Factor: Your Carbon Footprint Calculator")

    try:
        # Input for transportation
        mileage = float(input("Enter your total miles traveled in a year: "))
        fuel_efficiency = float(input("Enter your vehicle's fuel efficiency (mpg): "))
        fuel_type = input("Enter fuel type (gasoline/diesel): ")

        # Calculate transportation footprint
        transportation_fp = calculate_transportation_footprint(mileage, fuel_efficiency, fuel_type)

        # Input for energy
        kwh = float(input("Enter your total kWh energy consumption in a year: "))
        energy_source = input("Enter energy source (grid/renewable): ")

        # Calculate energy footprint
        energy_fp = calculate_energy_footprint(kwh, energy_source)

        # Input for waste
        pounds = float(input("Enter your total waste produced in a year (lbs): "))
        recycling_rate = float(input("Enter your recycling rate (%): "))

        # Calculate waste footprint
        waste_fp = calculate_waste_footprint(pounds, recycling_rate)

        # Total carbon footprint
        total_footprint = transportation_fp + energy_fp + waste_fp
        print(f"\nYour total annual carbon footprint is: {total_footprint:.2f} lbs of CO2")

        # Provide recommendations
        give_recommendations(transportation_fp, energy_fp, waste_fp)

    except ValueError as e:
        print(f"Input error: {e}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    main()
```

This program covers three key aspects of carbon footprint calculation: transportation, energy, and waste. It provides basic error handling and outputs suggestions based on the calculated carbon footprint. Note that the values for CO2 emissions per unit are illustrative, and for a production system, you should research and use detailed and specific factors.