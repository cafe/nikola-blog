.. title: Custom Domain Settings of Yandex Mail
.. slug: custom-domain-settings-of-yandex-mail
.. date: 2016-05-06 14:04:20 UTC+08:00
.. tags: domain
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

This post is talking about the steps needed to set up a custom domain mail account using Yandex Mail service.

As far as I know, Outlook.com (Microsoft) and Google have stopped their free services for custom domain mails. After a search, I found Yandex mail. Yandex Mail provides unlimited mail accounts (by default 1000 but you can apply more) with unlimited storage space. Also, Yandex allows custom logo in the web interface. The most important thing is: all of these features are free to use.

.. TEASER_END

Note: Yandex is originated from Russia though, but luckily it has English interface for easy access.

Here, I assume you already have your own domain prepared. Please follow these steps to use Yandex custom domain mail, **FOR FREE**:

1. log into your Yandex Mail, and go to https://domain.yandex.com/ to add your own domain, e.g., oxyz.org
2. Verify your domain according to the instructions of Yandex. If you are hosting your site using Github, the first option is the most convinient: just creating a ``.html`` file with specified string as content, and uploading to the Github server. It does not need to touch your DNS settings. BTW, this is my host records settings on *Namecheap.com*:

   .. image:: /images/custom-domain-settings-of-yandex-mail-hostrecords.png
      :width: 480

3. Mail server settings on your domain provider side (we just use *Namecheap.com* as an example, and please note that it may take several minutes to take effects):

   .. image:: /images/custom-domain-settings-of-yandex-mail-mailsettings.png
      :width: 480  

4. After the success of verifications, you are free to create email accouts with your own custom domain, as many as you want.
5. Log into your new email by visiting http://mail.yandex.com/for/yourdomain.com

All set. Just enjoy your own email address!

