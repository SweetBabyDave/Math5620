**Author:** David Merkley

**Language:** Python

**Description/Purpose:** This code solves an IVP using the Predictor Corrector Method. Then it solves for the exact solution and plots the error.

**Implementation/Code:** 

    from matplotlib import pyplot as plt
    import numpy as np

    # Function to get Exact solution
    def ExactSol(t):
        return np.e ** ((1/2) * (t**2) + t)

    # The initial value problem looked at
    def IVP(u, t):
        return (t + 1) * u

    # All of these k functions are to evaluate the Ufinal function
    def k1(U, t):
        return IVP(U, t)

    def k2(U, t):
        return IVP(U + (0.05 * k1(U, t)), t + 0.05)

    #  Returns a solution to the IVP with the Runge Kutta Method
    def Ufinal(U, t):
        return U + (0.05/2 * (k1(U, t) + k2(U, t)))

    def main():
        # Initiates lists required to plot the error of the solution
        listU = [1]
        listExact = [1]
        listError = []

        #  For loop to get the runge kutta solution and exact solution along with it
        for n in range(1, 21):
            listU.append(Ufinal(listU[n-1], (n-1) * 0.05))
            listExact.append(ExactSol(n * 0.05))

        # For loop to get the error of the solution
        for listU_i, listExact1_i in zip(listU, listExact):
            listError.append(listExact1_i - listU_i)

        # Plotting the Errors and Graphs for Comparison
        x1 = np.linspace(0, 1, 21)
        plt.title("Predictor Corrector Method vs Exact Solution")
        plt.xticks(x1)
        plt.plot(x1, listU, marker='o', label='Exact Solution')
        plt.plot(x1, listExact, marker='o', label='Predictor Corrector Method')
        plt.legend()
        plt.show()
        plt.title("Error of Predictor Corrector Method")
        plt.xticks(x1)
        plt.plot(x1, listError, marker='o', label='Error')
        plt.legend()
        plt.show()

    main()

**Output:**

![Predictor](https://user-images.githubusercontent.com/82894531/161406551-ab32970e-eae6-4f85-b1c9-faacc2f9302b.png)
![PredictorError](https://user-images.githubusercontent.com/82894531/161406554-07e2af07-7513-481d-acfc-4a8533693d2b.png)

