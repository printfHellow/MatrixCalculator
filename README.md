package p0074;

import java.util.Scanner;

public class P0074 {

    public static void main(String[] args) {
        P0074 program = new P0074();
        program.start();
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
        double[][] matrix1 = getMatrixInput(scanner, "1");
        double[][] matrix2 = getMatrixInput(scanner, "2", matrix1.length, matrix1[0].length, "cộng");
        if (matrix2 == null) return; // Nếu không có ma trận 2, quay lại menu
        double[][] result = additionMatrix(matrix1, matrix2);
        System.out.println("Kết quả của phép cộng:");
        displayMatrix(result);
    }

    public void performSubtraction(Scanner scanner) {
        double[][] matrix1 = getMatrixInput(scanner, "1");
        double[][] matrix2 = getMatrixInput(scanner, "2", matrix1.length, matrix1[0].length, "trừ");
        if (matrix2 == null) return; // Nếu không có ma trận 2, quay lại menu
        double[][] result = subtractionMatrix(matrix1, matrix2);
        System.out.println("Kết quả của phép trừ:");
        displayMatrix(result);
    }

    public void performMultiplication(Scanner scanner) {
        double[][] matrix1 = getMatrixInput(scanner, "1");
        System.out.print("Nhập số hàng cho Ma trận 2: ");
        int rows2 = getPositiveIntInput(scanner);
        System.out.print("Nhập số cột cho Ma trận 2: ");
        int columns2 = getPositiveIntInput(scanner);
        
        if (matrix1[0].length != rows2) {
            System.out.println("Số cột của ma trận đầu tiên phải bằng số hàng của ma trận thứ hai.");
            return;
        }

        double[][] matrix2 = getMatrixInput(scanner, "2", rows2, columns2, "nhân");
        if (matrix2 == null) return; // Nếu không có ma trận 2, quay lại menu
        double[][] result = multiplicationMatrix(matrix1, matrix2);
        System.out.println("Kết quả của phép nhân:");
        displayMatrix(result);
    }

    public static int getIntInput(Scanner scanner) {
        while (true) {
            try {
                return Integer.parseInt(scanner.next());
            } catch (NumberFormatException e) {
                System.out.println("Đầu vào không hợp lệ. Vui lòng nhập một số nguyên.");
            }
        }
    }

    public static int getPositiveIntInput(Scanner scanner) {
        while (true) {
            int input = getIntInput(scanner);
            if (input > 0) {
                return input;
            } else {
                System.out.println("Số phải là một số nguyên dương. Vui lòng nhập lại.");
            }
        }
    }

    public static double[][] getMatrixInput(Scanner scanner, String matrixOrder) {
        System.out.println("Nhập số hàng cho Ma trận " + matrixOrder + ": ");
        int rows = getPositiveIntInput(scanner);
        System.out.println("Nhập số cột cho Ma trận " + matrixOrder + ": ");
        int columns = getPositiveIntInput(scanner);
        return inputMatrix(scanner, rows, columns, matrixOrder);
    }

    public static double[][] getMatrixInput(Scanner scanner, String matrixOrder, int expectedRows, int expectedColumns, String operation) {
        System.out.println("Nhập số hàng cho Ma trận " + matrixOrder + ": ");
        int rows = getPositiveIntInput(scanner);
        System.out.println("Nhập số cột cho Ma trận " + matrixOrder + ": ");
        int columns = getPositiveIntInput(scanner);

        if (rows != expectedRows || columns != expectedColumns) {
            System.out.printf("Ma trận phải có kích thước %dx%d để thực hiện phép %s.\n", expectedRows, expectedColumns, operation);
            return null; // Nếu không thỏa mãn điều kiện, trả về null
        }

        return inputMatrix(scanner, rows, columns, matrixOrder);
    }

    public static double[][] inputMatrix(Scanner scanner, int rows, int columns, String matrixOrder) {
        double[][] matrix = new double[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                System.out.printf("Nhập Ma trận[%d][%d]: ", i + 1, j + 1);
                matrix[i][j] = getDoubleInput(scanner);
            }
        }
        return matrix;
    }

    public static double getDoubleInput(Scanner scanner) {
        while (true) {
            try {
                return Double.parseDouble(scanner.next());
            } catch (NumberFormatException e) {
                System.out.println("Đầu vào không hợp lệ. Vui lòng nhập một số thực.");
            }
        }
    }

    public static void displayMatrix(double[][] matrix) {
        for (double[] row : matrix) {
            for (double val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }

    public static double[][] additionMatrix(double[][] matrix1, double[][] matrix2) {
        int rows = matrix1.length;
        int columns = matrix1[0].length;
        double[][] result = new double[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                result[i][j] = matrix1[i][j] + matrix2[i][j];
            }
        }
        return result;
    }

    public static double[][] subtractionMatrix(double[][] matrix1, double[][] matrix2) {
        int rows = matrix1.length;
        int columns = matrix1[0].length;
        double[][] result = new double[rows][columns];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                result[i][j] = matrix1[i][j] - matrix2[i][j];
            }
        }
        return result;
    }

    public static double[][] multiplicationMatrix(double[][] matrix1, double[][] matrix2) {
        int rows1 = matrix1.length;
        int columns1 = matrix1[0].length;
        int columns2 = matrix2[0].length;
        double[][] result = new double[rows1][columns2];
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
