# nagios-notify-erb

A collection of nagios notification templates written in ERB.

## Usage:

### Enable Environment Macros:

Edit your nagios.cfg to enable environment macros:

    enable_environment_macros=1

### Update Notification Commands:

Edit your commands.cfg (or wherever you define your notification commands):

    define command {
      command_name notify-service-by-email
      command_line /usr/local/bin/erb /etc/nagios3/nagios-notify-erb/service-email.erb | /usr/sbin/sendmail -f$ADMINEMAIL$ $CONTACTEMAIL$
    }
    define command {
      command_name notify-service-by-sms
      command_line /usr/local/bin/erb /etc/nagios3/nagios-notify-erb/service-sms.erb | /usr/sbin/sendmail -f$ADMINEMAIL$ $CONTACTEMAIL$
    }
    define command {
      command_name notify-host-by-email
      command_line /usr/local/bin/erb /etc/nagios3/nagios-notify-erb/host-email.erb | /usr/sbin/sendmail -f$ADMINEMAIL$ $CONTACTEMAIL$
    }
    define command {
      command_name notify-host-by-sms
      command_line /usr/local/bin/erb /etc/nagios3/nagios-notify-erb/host-sms.erb | /usr/sbin/sendmail -f$ADMINEMAIL$ $CONTACTEMAIL$
    }

## Icinga

Icinga exports the same environment macros, with a different prefix. If you want to use
nagios-notify-erb templates with Icinga, replace all instances of NAGIOS with ICINGA in
the ENV[''] blocks within the erb files.
