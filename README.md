# Sending-Email-With-PHP-SMTP
# Sample code to send secured email with PHP SMTP

# For The Code To Work, You Have To Create A Real Email Account On Your Server.

# PHP
# SMTP

<?php
  
  $subject = 'Hi There';
  $message = 'This Is A Test Email With PHP';
  $to = 'receiver@email.com';
          
  //Send Email
  sendMail($to,$subject,$message);
          
  //Email Function
  function sendMail($email,$subject,$message){
        include('Mail.php'); 
        $adminEmail="account@email.com";
        
        $username = 'account@email.com'; // your email address
        $password = 'emailpassword'; // your email address password
        
        $from = $adminEmail;
        $to = $email;
        $body= $message;
        
        $headers = array ('From' => $from, 'To' => $to, 'Subject' => $subject); // the email headers
        $smtp = Mail::factory('smtp', array ('host' =>'localhost', 'auth' => true, 'username' => $username, 'password' => $password, 'port' => '25')); // SMTP protocol with the username and password of an existing email account in your hosting account
        $mail = $smtp->send($to, $headers, $body); // sending the email
        
        if (PEAR::isError($mail)){
        echo("<p>" . $mail->getMessage() . "</p>");
        }
        else {
        echo("<p>Message successfully sent!</p>");
        // header("Location: http://www.example.com/"); // you can redirect page on successful submission.
        }
    }

?>


