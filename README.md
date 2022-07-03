# NAME

Test::Rsyslog - Creates a temporary instance of rsyslog to run tests against

# VERSION

Version 0.06

# SYNOPSIS

     my $rsyslog = Test::Rsyslog->new();

     Sys::Syslog::setlogsock({ type => 'unix', path => $rsyslog->socket_path() });
     # or "Sys::Syslog::setlogsock('unix', $rsyslog->socket_path());" for older Sys::Syslogs
     Sys::Syslog::openlog('program[' . $$ . ']','cons','LOG_LOCAL7');
     Sys::Syslog::syslog('info|LOG_LOCAL7','This is a test message');
     Sys::Syslog::closelog();

     ok($rsyslog->find('This is a test message'), 'Rsyslog is okay');
    

# DESCRIPTION

This module allows easy creation and tear down of a rsyslog instance.  When the variable goes 
out of scope, the rsyslog instance is torn down and the file system objects it relies on are removed.

# SUBROUTINES/METHODS

## new

This method will setup and start the rsyslog instance.  It currently has no parameters, but this may change in response to feature requests

## socket\_path

This method returns that path to the UNIX file system socket that is connected to the current running instance of rsyslog

## find($string)

This method searches the existing logs that rsyslog has processed to see if a message has been found matching $string.  It will return a list of every line in the log file that matches $string.

## start

This method starts the rsyslog instance

## stop

This method stops the rsyslog instance

## alive

This method checks to make sure that the rsyslogd instance is still running

## messages

This method returns the content of the rsyslogd log file

## scrub

This method truncates the rsyslogd log file.  Rsyslogd must be stopped to truncate the log file

# DIAGNOSTICS

- `Failed to open %s for reading`

    There has been a file system error trying to read from the rsyslog logfile.

- `Failed to print to %s`

    There has been a file system error trying to write to the rsyslog configuration file.

- `Failed to fork`

    The operating system was unable to fork a subprocess for use by the rsyslog daemon.

- `Failed to rmdir %s`

    There has been a file system error trying to remove the temporary directory.

- `Failed to unlink %s`

    There has been a file system error trying to unlink a temporary file

- `Failed to close %s`

    There has been a file system error trying to close a temporary file

- `Failed to mkdir %s`

    There has been a file system error trying to make the temporary directory

- `Temporary rsyslog daemon is already running...`

    The rsyslog daemon has already started

- `Unable to truncate while rsyslogd is still running`

    This module will not truncate the messages file while rsyslogd could still be writing to it

- `Unable to untaint the directory path`

    The module generated an unrecognisable temporary path for rsyslogd

# CONFIGURATION AND ENVIRONMENT

Test::Rsyslog requires no configuration files or environment variables.

# DEPENDENCIES

Test::Rsyslog requires Perl 5.6 or better.

# INCOMPATIBILITIES

None reported

# BUGS AND LIMITATIONS

Please report any bugs or feature requests to `bug-test-rsyslog at rt.cpan.org`, or through
the web interface at [http://rt.cpan.org/NoAuth/ReportBug.html?Queue=Test-Rsyslog](http://rt.cpan.org/NoAuth/ReportBug.html?Queue=Test-Rsyslog).  I will be notified, and then you'll
automatically be notified of progress on your bug as I make changes.

# SUPPORT

You can find documentation for this module with the perldoc command.

    perldoc Test::Rsyslog

You can also look for information at:

- RT: CPAN's request tracker (report bugs here)

    [http://rt.cpan.org/NoAuth/Bugs.html?Dist=Test-Rsyslog](http://rt.cpan.org/NoAuth/Bugs.html?Dist=Test-Rsyslog)

- AnnoCPAN: Annotated CPAN documentation

    [http://annocpan.org/dist/Test-Rsyslog](http://annocpan.org/dist/Test-Rsyslog)

- CPAN Ratings

    [http://cpanratings.perl.org/d/Test-Rsyslog](http://cpanratings.perl.org/d/Test-Rsyslog)

- Search CPAN

    [http://search.cpan.org/dist/Test-Rsyslog/](http://search.cpan.org/dist/Test-Rsyslog/)

# AUTHOR

David Dick, `<ddick at cpan.org>`

# ACKNOWLEDGEMENTS

# LICENSE AND COPYRIGHT

Copyright 2017 David Dick.

This program is free software; you can redistribute it and/or modify it
under the terms of either: the GNU General Public License as published
by the Free Software Foundation; or the Artistic License.

See [http://dev.perl.org/licenses/](http://dev.perl.org/licenses/) for more information.
