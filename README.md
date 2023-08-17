# image-encryption-decryption
import javax.swing.*;
import java.awt.FlowLayout;
import java.io.File;
import java.awt.Font;
import java.io.FileInputStream;
import java.io.FilterOutputStream;


public class ImageOration {
   public static void operate(int key){
        JFileChooser fileChooser=new JFileChooser();
        fileChooser.showOpenDialog(null);
        File file=fileChooser.getSelectedFile();
        // file input stream reader

        try
        {

            FileInputStream fis =new FileInputStream(file);
            byte[]data=new byte[fis.available()];
            fis.read(data);
            int i=0;
            for (byte b:data)
            {
                System.out.println(b);
               data[i]=(byte)(b^key);
               i++;
            }
            FilterOutputStream fos = new FilterOutputStream(file);
            fos.write(data);
                fos.close();
            JOptionPane.showMessageDialog(null,"done");
        }catch(Exception e){
            e.printStackTrace();
        }

    }
    public static void main(String[] args) {
        System.out.println("hello");
        JFrame f =new JFrame();
        f.setTitle("Image Operation");
        f.setSize(300,300);
        f.setLocationRelativeTo(null);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Font font=new Font("Roboto",Font.BOLD,20);
        //
        JButton button=new JButton();
        button.setText("Open image");
        button.setFont(font);

        // creating text field
        JTextField textField=new JTextField(8);
        textField.setFont(font);
        button.addActionListener(e -> {
            System.out.println("button clicked");
            String text = textField.getText();
            int temp= Integer.parseInt(text);
            operate(temp);
        });
        f.setLayout(new FlowLayout());
        f.add(button);
        f.add(textField);
        f.setVisible(true);
    }
}
