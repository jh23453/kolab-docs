=============================
Frequently Answered Questions
=============================

Log Messages
============

.. seealso::

    *   :ref:`admin_faq_email-blocked-spamhaus`

Unable to open /etc/sasldb2
---------------------------

No :file:`user_deny.db`
-----------------------

IOERROR: opening /var/lib/imap/user_deny.db: No such file or directory

Anti-Spam
=========

No ``X-Spam`` Headers
---------------------

.. _admin_faq_email-blocked-spamhaus:

Email Blocked Using zen.spamhaus.org
------------------------------------

You are seeing the following in :file:`/var/log/maillog` (line breaks added for
legibility):

.. parsed-literal::

    NOQUEUE: reject: RCPT from unknown[3.2.1.0]: 554 5.7.1 Service \\
    unavailable; Client host [3.2.1.0] blocked using zen.spamhaus.org; \\
    from=<something@domain.tld>

This message indicates your SMTP server, receiving a message from the Internet,
has refused the message.

The sending host (at IP address 3.2.1.0) is blocked using a centralized,
external service (spamhaus.org), that keeps track of hosts and networks on the
Internet with a reputation of spamming.

For more information on this service, see http://www.spamhaus.org/zen/.

You will want to continue performing these checks, but just in case you do not
want to, the relevant setting in Postfix is:

.. parsed-literal::

    # postconf smtpd_sender_restrictions

It is the responsibility of the sending host to notify the original sender the
message was not delivered.
