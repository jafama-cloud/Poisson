# Poisson
Poisson Distribution Calculator

# Import necessary libraries
import scipy.stats as stats # for statistical functions
import matplotlib.pyplot as plt # for plotting graphs

# Function to calculate the Poisson probability for a specific value
def calculate_poisson_probability(lambda_param, specific_value):
    """
    Calculate the Poisson probability for a specific value.

    Parameters:
    - lambda_param (float): The λ parameter of the Poisson distribution (average rate).
    - specific_value (int): The specific value (k) for which the Poisson probability will be calculated.

    Returns:
    float: The Poisson probability for the specific value.
    """
    return stats.poisson.pmf(specific_value, lambda_param)

# Function to plot the Poisson distribution for a range of values
def plot_poisson_distribution(lambda_param, k_values):
    """
    Plot the Poisson distribution for a range of values.

    Parameters:
    - lambda_param (float): The λ parameter of the Poisson distribution (average rate).
    - k_values (list): List of specific values (k) for which the Poisson probabilities will be calculated and plotted.
    """
    # Create a subplot with a single plot
    fig, ax = plt.subplots(figsize=(8, 4))

    # Calculate Poisson probabilities for each k value
    x = range(min(k_values), max(k_values) + 1)
    poisson_probs = [stats.poisson.pmf(value, lambda_param) for value in x]

    # Plot the Poisson distribution
    ax.bar(x, poisson_probs)

    # Set x-axis and y-axis labels
    ax.set_xlabel("ƙ (the number of times an event occurs)")
    ax.set_ylabel("Probability\n")

    # Set the title of the plot
    ax.set_title(f"Poisson Distribution (λ = {lambda_param})")

    # Set x-axis ticks to specified k values
    ax.set_xticks(k_values)

    # Display the plot
    plt.show()


# Main program logic
def main():
    # Outer loop to run the program repeatedly until the user chooses to exit
    while True:
        try:
            # Input lambda (λ) parameter from the user
            lambda_param = float(input("Enter the lambda [λ] parameter (average rate): "))
            
            # Input the number of specific values (k) to calculate
            num_k_values = int(input("How many k values do you want to calculate? "))
            k_values = []

            # Input specific values (k) from the user and store them in a list
            for i in range(num_k_values):
                k = int(input(f"Enter k value {i + 1}: "))
                k_values.append(k)

            print(f"\nλ = {lambda_param}")
            print("k values with their respective probabilities:")

            # Calculate and display Poisson probabilities for the entered k values
            for k in k_values:
                poisson_prob = calculate_poisson_probability(lambda_param, k)
                print(f"k = {k}, Probability = {poisson_prob:.2f}")

            # Ask the user if they want to display the Poisson Distribution Graph
            choice = input("\nDo you want to display the Poisson Distribution Graph (Y/N)? ").strip().lower()

            # Inner loop to keep asking the user until they answer 'Y' or 'N'
            while choice not in ['y', 'n']:
                print("Invalid choice. Please enter 'Y' or 'N'.")
                choice = input("\nDo you want to display the Poisson Distribution Graph (Y/N)? ").strip().lower()

            # Display the graph if the user chooses 'Y'
            if choice == 'y':
                plot_poisson_distribution(lambda_param, k_values)
            elif choice == 'n':
                pass

            # Ask the user if they want to do another calculation or exit the program
            while True:
                another_choice = input("\nDo you want to do another calculation (Y/N)? ").strip().lower()

                if another_choice == 'y':
                    break  # Continue with the next calculation
                elif another_choice == 'n':
                    print("Exiting the program.")
                    exit()  # Terminate the program
                else:
                    print("Invalid choice. Please enter 'Y' or 'N'.")

        except ValueError:
            print("Invalid input. Please enter valid numeric values for lambda, k values, specific value, or range.")

# Execute the main program
if __name__ == "__main__":
    main()
