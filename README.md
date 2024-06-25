# MatrixCalculator
import java.util.Scanner;

public class MatrixCalculator {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            displayMenu();
            int option = getIntInput(scanner);
            switch (option) {
                case 1:
                    performAddition(scanner);
                    break;
                case 2:
                    performSubtraction(scanner);
                    break;
                case 3:
                    performMultiplication(scanner);
                    break;
                case 4:
                    System.out.println("Exiting program.");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    public static void displayMenu() {
        System.out.println("Select an option:");
        System.out.println("1. Add matrices");
        System.out.println("2. Subtract matrices");
        System.out.println("3. Multiply matrices");
        System.out.println("4. Exit");
        System.out.println("Your choice: ");
    }

    public static void performAddition(Scanner scanner) {
        int[][] matrix1 = getMatrixInput(scanner, "1");
        int[][] matrix2 = getMatrixInput(scanner, "2");
        if (matrix1.length == matrix2.length && matrix1[0].length == matrix2[0].length) {
            int[][] result = additionMatrix(matrix1, matrix2);
            System.out.println("Result of addition:");
            displayMatrix(result);
        } else {
            System.out.println("Matrices must have the same dimensions for addition.");
        }
    }

    public static void performSubtraction(Scanner scanner) {
        int[][] matrix1 = getMatrixInput(scanner, "1");
        int[][] matrix2 = getMatrixInput(scanner, "2");
        if (matrix1.length == matrix2.length && matrix1[0].length == matrix2[0].length) {
            int[][] result = subtractionMatrix(matrix1, matrix2);
            System.out.println("Result of subtraction:");
            displayMatrix(matrix1);
            System.out.println("-");
            displayMatrix(matrix2);
            System.out.println("=");
            displayMatrix(result);
        } else {
            System.out.println("Matrices must have the same dimensions for subtraction.");
        }
    }

    public static void performMultiplication(Scanner scanner) {
        int[][] matrix1 = getMatrixInput(scanner, "1");
        int[][] matrix2 = getMatrixInput(scanner, "2");
        if (matrix1[0].length == matrix2.length) {
            int[][] result = multiplicationMatrix(matrix1, matrix2);
            System.out.println("Result of multiplication:");
            displayMatrix(result);
        } else {
            System.out.println("Number of columns in the first matrix must be equal to the number of rows in the second matrix.");
        }
    }

    public static int getIntInput(Scanner scanner) {
        while (true) {
            try {
                return Integer.parseInt(scanner.next());
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
    }

    public static int[][] getMatrixInput(Scanner scanner, String matrixOrder) {
        System.out.print("Enter Row Matrix " + matrixOrder + ":");
        int rows = getIntInput(scanner);
        System.out.print("Enter Rolumn Matrix " + matrixOrder + ":");
        int columns = getIntInput(scanner);
        int[][] matrix = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                System.out.printf("Enter Matrix[%d][%d]: ", i+1, j+1);
                matrix[i][j] = getIntInput(scanner);
            }
        }
        return matrix;
    }

    public static void displayMatrix(int[][] matrix) {
        for (int[] row : matrix) {
            for (int val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }

    public static int[][] additionMatrix(int[][] matrix1, int[][] matrix2) {
        int rows = matrix1.length;
        int columns = matrix1[0].length;
        int[][] result = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                result[i][j] = matrix1[i][j] + matrix2[i][j];
            }
        }
        return result;
    }

    public static int[][] subtractionMatrix(int[][] matrix1, int[][] matrix2) {
        int rows = matrix1.length;
        int columns = matrix1[0].length;
        int[][] result = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                result[i][j] = matrix1[i][j] - matrix2[i][j];
            }
        }
        return result;
    }

    public static int[][] multiplicationMatrix(int[][] matrix1, int[][] matrix2) {
        int rows1 = matrix1.length;
        int columns1 = matrix1[0].length;
        int columns2 = matrix2[0].length;
        int[][] result = new int[rows1][columns2];
        for (int i = 0; i < rows1; i++) {
            for (int j = 0; j < columns2; j++) {
                for (int k = 0; k < columns1; k++) {
                    result[i][j] += matrix1[i][k] * matrix2[k][j];
                }
            }
        }
        return result;
    }
}
