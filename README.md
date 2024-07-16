# MatrixCalculator
import java.util.Scanner;

public class MatrixCalculator {

    public static void main(String[] args) {
        MatrixCalculator calculator = new MatrixCalculator();
        calculator.start();
    }

    public void start() {
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
                case 4:
                    performPowerMinusOne(scanner);
                    break;
                    
                case 5:
                    System.out.println("Thoát chương trình.");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Lựa chọn không hợp lệ. Vui lòng thử lại.");
            }
        }
    }

    public static void displayMenu() {
        System.out.println("Chọn một tùy chọn:");
        System.out.println("1. Cộng ma trận");
        System.out.println("2. Trừ ma trận");
        System.out.println("3. Nhân ma trận");
        System.out.println("4. Thoát");
        System.out.print("Lựa chọn của bạn: ");
    }

    public void performAddition(Scanner scanner) {
        int[][] matrix1 = getMatrixInput(scanner, "1");
        int[][] matrix2 = getMatrixInput(scanner, "2");
        if (matrix1.length == matrix2.length && matrix1[0].length == matrix2[0].length) {
            int[][] result = additionMatrix(matrix1, matrix2);
            System.out.println("Kết quả của phép cộng:");
            displayMatrix(result);
        } else {
            System.out.println("Ma trận phải có cùng kích thước để thực hiện phép cộng.");
        }
    }

    public void performSubtraction(Scanner scanner) {
        int[][] matrix1 = getMatrixInput(scanner, "1");
        int[][] matrix2 = getMatrixInput(scanner, "2");
        if (matrix1.length == matrix2.length && matrix1[0].length == matrix2[0].length) {
            int[][] result = subtractionMatrix(matrix1, matrix2);
            System.out.println("Kết quả của phép trừ:");
            displayMatrix(result);
        } else {
            System.out.println("Ma trận phải có cùng kích thước để thực hiện phép trừ.");
        }
    }

    public void performMultiplication(Scanner scanner) {
        int[][] matrix1 = getMatrixInput(scanner, "1");
        int[][] matrix2 = getMatrixInput(scanner, "2");
        if (matrix1[0].length == matrix2.length) {
            int[][] result = multiplicationMatrix(matrix1, matrix2);
            System.out.println("Kết quả của phép nhân:");
            displayMatrix(result);
        } else {
            System.out.println("Số cột của ma trận đầu tiên phải bằng số hàng của ma trận thứ hai.");
        }
    }
     public void performPowerMinusOne(Scanner scanner) {
        int[][] matrix = getMatrixInput(scanner, "");
        System.out.print("Nhập số mũ: ");
        int exponent = getIntInput(scanner);
        int[][] powerMatrix = powerMatrix(matrix, exponent);
        int[][] result = subtractOneFromMatrix(powerMatrix);
        System.out.println("Kết quả của ma trận mũ trừ 1:");
        displayMatrix(result);
    }

    public static int getIntInput(Scanner scanner) {
        while (true) {
            try {
                return Integer.parseInt(scanner.next());
            } catch (NumberFormatException e) {
                System.out.println("Đầu vào không hợp lệ. Vui lòng nhập một số.");
            }
        }
    }

    public static int[][] getMatrixInput(Scanner scanner, String matrixOrder) {
        System.out.print("Nhập số hàng cho Ma trận " + matrixOrder + ": ");
        int rows = getIntInput(scanner);
        System.out.print("Nhập số cột cho Ma trận " + matrixOrder + ": ");
        int columns = getIntInput(scanner);
        int[][] matrix = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                System.out.printf("Nhập Ma trận[%d][%d]: ", i + 1, j + 1);
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
     public static int[][] powerMatrix(int[][] matrix, int exponent) {
        int rows = matrix.length;
        int columns = matrix[0].length;
        int[][] result = new int[rows][columns];
        
        // Initialize result as identity matrix
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                result[i][j] = (i == j) ? 1 : 0;
            }
        }

        int[][] base = matrix;
        while (exponent > 0) {
            if (exponent % 2 == 1) {
                result = multiplicationMatrix(result, base);
            }
            base = multiplicationMatrix(base, base);
            exponent /= 2;
        }
        return result;
    }

    public static int[][] subtractOneFromMatrix(int[][] matrix) {
        int rows = matrix.length;
        int columns = matrix[0].length;
        int[][] result = new int[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                result[i][j] = matrix[i][j] - 1;
            }
        }
        return result;
    }
}
