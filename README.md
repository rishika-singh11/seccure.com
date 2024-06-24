# seccure.com
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.*;

public class SecureComApp extends JFrame {

    private JTextField inputField;
    private JTextArea outputArea;
    private JButton encryptButton;
    private JButton decryptButton;

    public SecureComApp() {
        setTitle("SECURE.COM");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        inputField = new JTextField();
        outputArea = new JTextArea();
        outputArea.setEditable(false);
        
        encryptButton = new JButton("Encrypt");
        decryptButton = new JButton("Decrypt");

        encryptButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String input = inputField.getText();
                String encrypted = encrypt(input, 3); // Simple Caesar Cipher with shift 3
                outputArea.setText("Encrypted: " + encrypted);
            }
        });

        decryptButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String input = inputField.getText();
                String decrypted = decrypt(input, 3); // Simple Caesar Cipher with shift 3
                outputArea.setText("Decrypted: " + decrypted);
            }
        });

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(3, 1));
        panel.add(inputField);
        panel.add(encryptButton);
        panel.add(decryptButton);

        add(panel, BorderLayout.NORTH);
        add(new JScrollPane(outputArea), BorderLayout.CENTER);
    }

    private String encrypt(String text, int shift) {
        StringBuilder result = new StringBuilder();
        for (char character : text.toCharArray()) {
            if (Character.isLetter(character)) {
                char base = Character.isLowerCase(character) ? 'a' : 'A';
                character = (char) ((character - base + shift) % 26 + base);
            }
            result.append(character);
        }
        return result.toString();
    }

    private String decrypt(String text, int shift) {
        return encrypt(text, 26 - shift); // Decryption for Caesar Cipher
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new SecureComApp().setVisible(true);
            }
        });
    }
}
