# reservation_system

import java.util.Arrays;
import java.util.Scanner;


class Cinema {



        static Scanner scanner = new Scanner(System.in);
        static int instanceCounter = 0;
        static int currentIncomeCounter = 0;
        static int totalIncome = 0;

        public static void main(String[] args) {



                char[][] board = createBoard();

                int choice = -1;


                while (choice != 0) {
                        System.out.println("1. Show the seats");
                        System.out.println("2. Buy a ticket");
                        System.out.println("3. Statistics");
                        System.out.println("0. Exit");

                        choice = scanner.nextInt();

                        switch (choice) {
                                case 1:
                                        printBoard(board);
                                        break;
                                case 2:
                                        buyTicket(board);
                                        instanceCounter++;
                                        break;
                                case 3:
                                        Statistics(board);
                                        break;
                        }


                }

        }


        public static char[][] createBoard() {

                System.out.print("Enter the number of rows: ");

                int rows = scanner.nextInt();

                System.out.print("Enter the number of seats in each row: ");

                int seats = scanner.nextInt();

                char[][] board = new char[rows][seats];

                for (char[] chars : board) {
                        Arrays.fill(chars, 'S');
                }

                return board;

        }

        public static void printBoard(char[][] board) {

                System.out.println("Cinema:");
                System.out.print("  ");
                for (int i = 1; i <= board[0].length; i++) {
                        System.out.print(i + " ");
                }
                System.out.println();
                for (int i = 0; i < board.length; i++) {
                        System.out.print(i + 1 + " ");
                        for (int j = 0; j < board[i].length; j++) {
                                System.out.print(board[i][j] + " ");
                        }
                        System.out.println();
                }
                System.out.println();

        }

        public static void buyTicket(char[][] board) {
                int rowChosen;
                int seatChosen;
                while (true) {
                        System.out.print("Enter a row number: ");
                        rowChosen = scanner.nextInt();

                        System.out.print("Enter a seat number in that row: ");

                        seatChosen = scanner.nextInt();

                        if (rowChosen <= board.length && seatChosen <= board.length ) {
                                if (board[rowChosen - 1][seatChosen - 1] == 'B') {
                                        System.out.println("That ticket has already been purchased!");
                                        System.out.println();
                                        continue;

                                } else if (board[rowChosen - 1][seatChosen - 1] == 'S') {
                                        System.out.println("Ticket reserved!");




                                } else {


                                System.out.println("Wrong input!");
                                instanceCounter--;
                                continue;
                                }

                                break;

                         } else {
                                System.out.println("Wrong input!");
                                continue;


                        }


                        }


                if (instanceCounter < 0) {
                        instanceCounter = 0 ;
                }


                int ticketPrice;


                if (board.length * board[0].length <= 60) {
                        ticketPrice = 10;
                        currentIncomeCounter += 10;

                } else {
                        int front = board.length / 2;
                        if (rowChosen - 1 < front) {
                                ticketPrice = 10;
                                currentIncomeCounter += 10;

                        } else {
                                ticketPrice = 8;
                                currentIncomeCounter +=8;
                        }
                }
                System.out.println();
                System.out.println("Ticket price: $" + ticketPrice);
                System.out.println();
                board[rowChosen - 1][seatChosen - 1] = 'B';
        }

        public static void Statistics(char[][] board) {
                float counter = instanceCounter;
                float result = counter / (board.length * board[0].length) * 100;
                String percent = String. format("%.2f", result);

                int front = board.length / 2;
                int back = board.length - front;

                if (board.length * board[0].length <= 60) {
                        totalIncome = board.length * board[0].length * 10;
                } else {
                        totalIncome = (front * board.length * 10) + (back * board.length * 8);
                }


                System.out.println();
                System.out.println("Number of purchased tickets: " + instanceCounter);
                System.out.println("Percentage: " + percent + "%");
                System.out.println("Current income: $" + currentIncomeCounter);
                System.out.println("Total income: $" + totalIncome);
                System.out.println();


        }

}
