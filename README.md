import java.util.Scanner;

class Product {
    int id;
    String name;
    double price;
    String category;

    Product(int id, String name, double price, String category) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.category = category;
    }
}

class ShoppingApp {   // removed public

    static void display(Product[] p, int n) {
        System.out.println("\nProduct List:");
        for (int i = 0; i < n; i++) {
            System.out.println(p[i].id + " | " + p[i].name + " | " + p[i].price + " | " + p[i].category);
        }
    }

    static void selectionSort(Product[] p, int n) {
        for (int i = 0; i < n - 1; i++) {
            int min = i;
            for (int j = i + 1; j < n; j++) {
                if (p[j].price < p[min].price) {
                    min = j;
                }
            }
            Product temp = p[i];
            p[i] = p[min];
            p[min] = temp;
        }
        System.out.println("\nSorted Successfully!");
    }

    static int binarySearch(Product[] p, int n, double key) {
        int low = 0, high = n - 1;
        while (low <= high) {
            int mid = (low + high) / 2;

            if (p[mid].price == key)
                return mid;
            else if (key < p[mid].price)
                high = mid - 1;
            else
                low = mid + 1;
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of products: ");
        int n = sc.nextInt();

        Product[] p = new Product[n];

        for (int i = 0; i < n; i++) {
            System.out.println("\nEnter Product " + (i + 1));

            System.out.print("ID: ");
            int id = sc.nextInt();

            System.out.print("Name: ");
            String name = sc.next();

            System.out.print("Price: ");
            double price = sc.nextDouble();

            System.out.print("Category: ");
            String category = sc.next();

            p[i] = new Product(id, name, price, category);
        }

        int choice;

        do {
            System.out.println("\n1.Display\n2.Sort\n3.Search\n4.Exit");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    display(p, n);
                    break;

                case 2:
                    selectionSort(p, n);
                    break;

                case 3:
                    System.out.print("Enter price: ");
                    double key = sc.nextDouble();

                    int res = binarySearch(p, n, key);

                    if (res != -1)
                        System.out.println("Found: " + p[res].name);
                    else
                        System.out.println("Not Found");
                    break;
            }

        } while (choice != 4);

        sc.close();
    }
}
