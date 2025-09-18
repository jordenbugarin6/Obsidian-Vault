```bash
Hi Jorden,  
   
My name is Raul, and I am a Student Mentor at Offsec.  
   
Taking the OSWA exam is a significant achievement, as it reveals your determination. I encourage you to keep learning and focus on areas where you can improve.  
In this email, I will provide you with both general and customized recommendations to aid you as you regroup for your next exam attempt: 

#### **General Suggestions**

·         Time Management

·         **Setting a timer**: Spending "X" hours on a machine. Make sure that you have enough/even time to review all of the machines and not stick with the same machine for the entire exam time.

·         **Using 3x3 and 5x5 method:** Upon Discovery, you dedicate three minutes to testing three exploit variations, unless you're almost certain, then move on. Avoid getting overly fixated by cycling through all boxes and potential entry points. Return to promising areas for a more thorough five-minute, five-technique session.

·         During your exam, we strongly recommend checking out the course material line by line to see if there was any text/module lab/capstone lab similar to what you are facing in the exam. It's an open book exam!

·         I  suggest checking the walkthrough streaming sessions to see the gaps in your enumeration: [https://www.youtube.com/watch?v=O8AwNa1tnMA&list=PLJrSyRNlZ2Ecrihsz_H5mXYoCmWZDqXyI&index=17](https://www.youtube.com/watch?v=O8AwNa1tnMA&list=PLJrSyRNlZ2Ecrihsz_H5mXYoCmWZDqXyI&index=17)

·         I highly suggest reviewing the OSA-WEB-200 recording videos as our Academy team taught the techniques and methodologies that learners could utilize when they are conducting black-box web app penetration testing: [https://portal.offsec.com/courses/osa-web-200/books-and-videos/modules](https://portal.offsec.com/courses/osa-web-200/books-and-videos/modules%C2%A0)

·         **Your best teacher is your last**: Please don't be discouraged. It took many of our OSCP-certified alumni to attempt the exam more than once.

1.      [**Reflections on Failure, Part One**](https://www.offsec.com/offsec/reflections-on-failure-one/)

2.      [**Reflections on Failure, Part Two**](https://www.offsec.com/offsec/reflections-on-failure-two/)

#### **Customized Suggestions**

·         **Challenge Labs**: Jubula, Mentor, Screaming Firehawk, Bubo and Piano

·         **Modules**: Cross-Origin Attacks, XML External Entities, Server-Side Request Forgery and Insecure Direct Object Reference

·         **Vulnerability exploitation order**: List all the vulnerabilities for obtaining access to the Admin UI and the ones for obtaning RCE. If you are attempting a vulnerability for getting RCE but you have not obtained access to admin UI, most probably your approach needs to be adjusted.

·         **Client Side Attacks**: In some cases, our exam developers also place some clues/texts to avoid any rabbit holes. Make sure to carefully review anything on the application as it can put you in the right path. The general rule for client-side attack is that the victim has to view/execute your payload.

·         Make sure to have a proper enumeration by fuzzing any files and directories.

·         Find out the available features by your enumeration and simply browsing the pages.

·         Discover each available feature such as creating a user, deleting a user and changing a password as an example.

·         While doing the above, make sure to intercept the requests and examine each parameter for any potential foothold.

·         Change the parameter values which you can control in your GET/POST requests to the application and see the behavior of the web application.

·         If you are dealing with an authentication bypass vulnerability, keep always in mind what you can do to get access to the application such as obtaining a password, changing a password of existence user or even obtaining a cookie.

·         **Automated tools**: While you are welcome to use any automated tools, you still have to consider:

·         Command Instructions should be very clear for the automated tools. Otherwise, they might just fail.

·         Automated tools should never replace manual testing specially in the discovery phase. You may still want to test the identification of the vulnerability manually and then proceed with automated tools for the exploitation steps.

 **Conclusion**  
   
Your success is our success!  
I wish you the best of luck as you reengage in your learning journey and next exam attempt!
```