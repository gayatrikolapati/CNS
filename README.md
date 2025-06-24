1.Fibonacci

import java.util.Scanner;
public class fibonacci 
{
	static int fibRecursive(int n) 
	{ 
		return n <= 2 ? 1 : fibRecursive(n - 1) + fibRecursive(n - 2); 
	}
	static int fibIterative(int n) 
	{
		int a = 1, b = 1;
		for (int i = 3; i <= n; i++) 
		{
			int c = a + b; a = b; b = c; 
		}
		return n <= 2 ? 1 : b;
	}
	public static void main(String[] args) 
	{
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter n: ");
		int n = scanner.nextInt();
		System.out.println("Recursive: " + fibRecursive(n) + ", Iterative: " + fibIterative(n));
	}
}

2.Prime numbers

import java.util.Scanner;
public class prime 
{
public static void main(String[] args) 
{
Scanner sc = new Scanner(System.in);
System.out.print("Enter an integer: ");
int limit = sc.nextInt();
for (int i = 2; i <= limit; i++) 
{
if (isPrime(i)) System.out.print(i + " ");
}
}
static boolean isPrime(int n) 
{
for (int i = 2; i * i <= n; i++) if (n % i == 0) return false;
return n > 1;
}
}

3.Palindrome

import java.util.Scanner;
public class palindrome 
{
public static void main(String[] args) 
{
Scanner sc = new Scanner(System.in);
System.out.print("Enter a string: ");
String str = sc.nextLine().toLowerCase();
System.out.println(str.equals(new StringBuilder(str).reverse().toString()) ? "Palindrome" : "Not a Palindrome");
}
}

4.Sorting

import java.util.*;
public class sorting {
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
System.out.println("Enter the number of names followed by the names:");
String[] names = new String[sc.nextInt()]; sc.nextLine();
for (int i = 0; i < names.length; i++) names[i] = sc.nextLine();
Arrays.sort(names);
System.out.println("Sorted Names:");
Arrays.stream(names).forEach(System.out::println);
}
}

5.runtime polymorphism

class shape
{
	void perimeter()
	{
		System.out.println("Total Surrounding Length");
	}
}

class square extends shape
{
	@Override
	void perimeter()
	{
		System.out.println("Perimeter of Square : 4 * Side");
	}
}

class rectangle extends shape
{
	@Override
	void perimeter()
	{
		System.out.println("Perimeter of Rectangle : 2 * (Length + Breadth)");
	}
}

public class rtPolymorphism
{
	public static void main(String args[])
	{
		shape myShape;
		myShape = new square();
		myShape.perimeter();
		myShape = new rectangle();
		myShape.perimeter();
	}
}

6.Packages...

User-defined :

Package Code:

package mypackage;
public class MyClass {
public void displayMessage() {
System.out.println("Hello from MyClass in mypackage!");
}
}

to use user-defined package, code:

import mypackage.MyClass;
public class newPackage {
public static void main(String[] args) {
MyClass obj = new MyClass();
obj.displayMessage();
}
}

Pre-defined :

import java.util.Scanner;
import java.util.Random;
import java.text.SimpleDateFormat;
import java.util.Date;
public class predefinedpackages
{
public static void main(String[] args)
{
Scanner scanner = new Scanner(System.in);
System.out.print("Enter your name: ");
String name = scanner.nextLine();
Random random = new Random();
int randomNumber = random.nextInt(100);
Date currentDate = new Date();
SimpleDateFormat formatter = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss");
String formattedDate = formatter.format(currentDate);
System.out.println("\nHello, " + name + "!");
System.out.println("Your lucky number today is: " + randomNumber);
System.out.println("Current Date and Time: " + formattedDate);
scanner.close();
}
}

7.StringTokenizer

import java.util.Scanner;
import java.util.StringTokenizer;
public class StrTok
{
public static void main(String[] args)
{
System.out.print("Enter values separated by Space: ");
Scanner scanner = new Scanner(System.in);
StringTokenizer tokenizer=new StringTokenizer(scanner.nextLine());
int sum=0;
while(tokenizer.hasMoreTokens())
sum+=Integer.parseInt(tokenizer.nextToken());
System.out.println("Sum: "+sum);
scanner.close();
}
}

8.File Information

import java.io.*;
import java.util.Scanner;
public class fileinfo
{
	public static void main( String args[] )
	{
		Scanner sc = new Scanner( System.in );
		System.out.print("Enter File Name: ");
		File file = new File( sc.nextLine() );
		if( file.exists() )
		{
			System.out.println("File exists: Yes");
			System.out.println("Readable: " + file.canRead() );
			System.out.println("Writable: " + file.canWrite());
			System.out.println("Type : " + ( file.isDirectory() ? "Directory" : "File" ) );
			System.out.println("Size : " + file.length() + " bytes\n\nContent: ");
			try( FileInputStream fis = new FileInputStream( file ) )
			{
				System.out.println( new String( fis.readAllBytes() ) );
			}
			catch( IOException e )
			{
				System.out.println("Error reading File : " + e.getMessage() );
			}
		}
		else System.out.println("File does not exist.");
		sc.close();
	}
}

9.File Analyser

import java.io.*;
import java.util.Scanner;
public class fileanalyse
{
	public static void main( String args[] )
	{
		Scanner sc = new Scanner( System.in );
		System.out.print("Enter File Name: ");
		String fileName = sc.nextLine();
		sc.close();
		try( BufferedReader br = new BufferedReader( new FileReader( fileName ) ) )
		{
			int charCount = 0, wordCount=0, lineCount=0;
			String line;
			while( ( line = br.readLine() ) != null )
			{
				lineCount++;
				charCount += line.length();
				wordCount += line.split("\\s+").length;
			}
			System.out.println("Characters: " + charCount + ", Words: " + wordCount + ", Lines: " + lineCount );
		}
		catch(IOException e)
		{
			System.out.println("Error: " + e.getMessage() );
		}
	}
}

10.File Viewer

import javax.swing.*;
import java.awt.*;
import java.io.*;
public class FileViewer extends JFrame {
    JTextArea textArea = new JTextArea(20, 50);

    public FileViewer() {
        JButton openButton = new JButton("Open File");
        openButton.addActionListener(e -> {
            JFileChooser fc = new JFileChooser();
            if (fc.showOpenDialog(this) == JFileChooser.APPROVE_OPTION)
                readFile(fc.getSelectedFile());
        });
        add(openButton, BorderLayout.NORTH);
        add(new JScrollPane(textArea), BorderLayout.CENTER);
        setTitle("APPLET : File Viewer");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        pack();
        setVisible(true);
    }

    private void readFile(File file) {
        try (BufferedReader r = new BufferedReader(new FileReader(file))) {
            textArea.setText(r.lines().reduce("", (a, b) -> a + b + "\n"));
        } catch (IOException ex) {
            textArea.setText("Error: " + ex.getMessage());
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(FileViewer::new);
    }
}

11.Calculator

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Calculator extends JFrame implements ActionListener {
    private JTextField display;
    private double num1, num2;
    private char operator;

    public Calculator() {
        setTitle("Simple Calculator");
        setSize(280, 350);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        display = new JTextField();
        display.setEditable(false);
        display.setFont(new Font("Arial", Font.BOLD, 18));
        display.setHorizontalAlignment(JTextField.RIGHT);
        display.setPreferredSize(new Dimension(280, 50));
        add(display, BorderLayout.NORTH);

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(5, 3, 5, 5));

        String[] buttons = {"7", "8", "9", "/", "4", "5", "6", "*", "1", "2", "3", "-", "0", "%", "=", "+", "C"};

        for (String text : buttons) {
            JButton button = new JButton(text);
            button.setFont(new Font("Arial", Font.BOLD, 16));
            button.addActionListener(this);
            panel.add(button);
        }

        add(panel, BorderLayout.CENTER);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String command = e.getActionCommand();

        if (Character.isDigit(command.charAt(0))) {
            display.setText(display.getText() + command);
        } else if (command.equals("C")) {
            display.setText("");
            num1 = num2 = 0;
        } else if (command.equals("=")) {
            num2 = Double.parseDouble(display.getText());
            String result;
            switch (operator) {
                case '+': result = String.valueOf(num1 + num2); break;
                case '-': result = String.valueOf(num1 - num2); break;
                case '*': result = String.valueOf(num1 * num2); break;
                case '/': result = (num2 == 0) ? "Can't divide by zero" : String.valueOf(num1 / num2); break;
                case '%': result = (num2 == 0) ? "Can't divide by zero" : String.valueOf(num1 % num2); break;
                default: result = "";
            }
            display.setText(result);
        } else {
            num1 = Double.parseDouble(display.getText());
            operator = command.charAt(0);
            display.setText("");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            Calculator calculator = new Calculator();
            calculator.setVisible(true);
        });
    }
}

12.Mouse Events

import javax.swing.*;
import java.awt.event.*;
public class MouseEvents extends JFrame 
{
    public MouseEvents() 
    {
        JLabel label = new JLabel("Perform a mouse action");
        add(label);
        setSize(400, 300);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setVisible(true);
        addMouseListener(new MouseAdapter() 
	{
            public void mouseClicked(MouseEvent e) { label.setText("Clicked at (" + e.getX() + ", " + e.getY() + ")"); }
            public void mousePressed(MouseEvent e) { label.setText("Pressed"); }
            public void mouseReleased(MouseEvent e) { label.setText("Released"); }
            public void mouseEntered(MouseEvent e) { label.setText("Entered"); }
            public void mouseExited(MouseEvent e)  { label.setText("Exited"); }
        }
	);
    }
    public static void main(String[] args) 
    {
        SwingUtilities.invokeLater(MouseEvents::new);
    }
}

13. Thread Life cycle

class MyThread extends Thread {
    public void run() {
        try { Thread.sleep(500); } catch (Exception e) {}
        System.out.println("Thread finished.");
    }
}

public class ThreadLifeCycle {
    public static void main(String[] args) throws Exception {
        MyThread t = new MyThread();
        System.out.println("State after creation: " + t.getState());
        t.start();
        System.out.println("State after start(): " + t.getState());
        Thread.sleep(100);
        System.out.println("State while running: " + t.getState());
        t.join();
        System.out.println("State after completion: " + t.getState());
    }
}

14.pie chart

import javax.swing.*;
import java.awt.*;
import java.util.*;
public class PieChart extends JFrame {
    ArrayList<String> labels = new ArrayList<>();
    ArrayList<Integer> values = new ArrayList<>();
    public PieChart() {
        JTextField lField = new JTextField(6);
        JTextField vField = new JTextField(3);
        JButton btn = new JButton("Add");
        btn.addActionListener(e -> {
            try {
                labels.add(lField.getText());
                values.add(Integer.parseInt(vField.getText()));
                lField.setText(""); vField.setText(""); repaint();
            } catch (Exception ex) {}
        });
        JPanel top = new JPanel();
        top.add(new JLabel("Label:"));
        top.add(lField);
        top.add(new JLabel("Value:"));
        top.add(vField);
        top.add(btn);
        add(top, "North");
        add(new JPanel() {
            protected void paintComponent(Graphics g) {
                int sum = values.stream().mapToInt(i -> i).sum();
                int angle = 0;
                for (int i = 0; i < values.size(); i++) {
                    int a = (int) Math.round((double) values.get(i) * 360 / sum);
                    g.setColor(Color.getHSBColor(i / 10f, .7f, .9f));
                    g.fillArc(100, 100, 200, 200, angle, a); 
                    angle += a;
                    g.fillRect(320, 100 + i * 15, 10, 10);
                    g.setColor(Color.BLACK);
                    g.drawString(labels.get(i), 335, 110 + i * 15);
                }
            }
        }, "Center");
        setSize(450, 450);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setVisible(true);
    }
    public static void main(String[] a) {
        SwingUtilities.invokeLater(PieChart::new);
    }
}

15. queue

import java.util.*;

class QE extends Exception { QE(String m) { super(m); } }

class Q {
    int[] q; int f = 0, r = -1;
    Q(int n) { q = new int[n]; }

    void enq(int x) throws QE {
        if (r == q.length - 1) throw new QE("Full");
        q[++r] = x;
    }

    int deq() throws QE {
        if (f > r) throw new QE("Empty");
        return q[f++];
    }

    void show() {
        for (int i = f; i <= r; i++) System.out.print(q[i] + " ");
        System.out.println();
    }
}

public class Queue {
    public static void main(String[] a) {
        Scanner sc = new Scanner(System.in);
        Q q = new Q(3);
        while (true) {
            System.out.print("1-Enq 2-Deq 3-Show 4-Exit: ");
            int ch = sc.nextInt();
            try {
                if (ch == 1) q.enq(sc.nextInt());
                else if (ch == 2) System.out.println("Out: " + q.deq());
                else if (ch == 3) q.show();
                else if (ch == 4) break;
            } catch (QE e) {
                System.out.println(e.getMessage());
            }
        }
    }
}
