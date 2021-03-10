public static void enviarConGMail2(String contenido,String origen,String destino) throws IOException {
		String correoPass=recogerpass();
		String correo=correoPass.split(".com")[0];
		final String correo2=correo+".com";
		String pass= correoPass.split(".com")[1];
		System.out.println(correo2);
		System.out.println(pass);
		
	    // Esto es lo que va delante de @gmail.com en tu cuenta de correo. Es el remitente también.
	    String remitente =correo2;  //Para la dirección nomcuenta@gmail.com
if(destino=="admin@empresa.com"||destino=="marketing@empresa.com"||destino=="contabilidad@empresa.com"||destino=="comercial@empresa.com"||destino=="webmaster@empresa.com") {
	
}else {
	destino="nada";
	return;
}
	    Properties props =new Properties();
	       props.put("mail.smtp.auth", "true");
	       props.put("mail.smtp.starttls.enable","true");
	       props.put("mail.smtp.host","smtp.gmail.com");
	       //props2.put("mail.smtp.ssl.trust", "smtp.gmail.com");
	       props.put("mail.smtp.port","587");
	       props.put("mail.smtps.socketFactory.port", "587");

	    Session session = Session.getDefaultInstance(props);
	    MimeMessage message = new MimeMessage(session);

	    try {     
	
	        Properties props2 =new Properties();
	          props2.put("mail.smtp.auth", "true");
	          props2.put("mail.smtp.starttls.enable","true");
	          props2.put("mail.smtp.host","smtp.gmail.com");
	          //props2.put("mail.smtp.ssl.trust", "smtp.gmail.com");
	          props2.put("mail.smtp.port","587");
	          props2.put("mail.smtps.socketFactory.port", "587");
	          Session session2 = Session.getInstance(props2,new javax.mail.Authenticator(){
	           protected PasswordAuthentication getPasswordAuthentication(){
	            return new PasswordAuthentication(correo2,pass);
	           }
	          });
	          
	       File miDir=new File("");
	       String directorio=miDir.getAbsolutePath();
	       
	       MimeMultipart multiparte=new MimeMultipart();
	       BodyPart texto=new MimeBodyPart();
	       String empresa=("codigoEmpresa");
	       String linea = "tienes un mensaje de:"+origen+"Dice: "+contenido;
	       texto.setText(linea);
	       
	       multiparte.addBodyPart(texto);
	        message = new MimeMessage(session2);
	       message.setFrom(new InternetAddress(destino));
	   	message.setRecipients(Message.RecipientType.TO, InternetAddress.parse(destino));
	       message.setSubject("Consulta sobre producto");
	       message.setContent(linea, "text/html");
	       Transport t=session2.getTransport("smtp");
	       t.connect("smtp.gmail.com",correo2,pass);
	   	t.sendMessage(message,message.getAllRecipients());
	          t.close();
	      } catch (MessagingException e) {
	   	   	 
	       e.printStackTrace();
	      
	       
	     }
	}
	
}
