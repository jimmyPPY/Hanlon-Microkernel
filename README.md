This project contains the Ruby scripts/classes that are used to
control the Razor Microkernel (and that interact with the Razor server).
The files contained in this project are bundled into the current version
of the Razor Microkernel (v0.8.4.0).  There are three primary services that
are included in this project that are started up during the Microkernel boot
process.  Those services include:

      1. The Configuration Agent, which can be found in the
         configuration-agent directory

      2. The Razor Microkernel Controller, which is actually contained
         in the rz_mk_control_server.rb file (which is, in turn, started
         up and controlled using the "Ruby Daemons" interface defined in
         the rz_mk_controller.rb file)

      3. The Razor Microkernel Web Server, which can be found in the
         rz_mk_web_server.rb file and which is used (along with the
         Configuration Agent) to push configuration changes from the
         Razor Server to the Razor Microkernel instances.

In addition, this project also includes a number of additional ruby files
and configuration files that are used by these services, a set of gems and
bundles that are installed dynamically each time that the Microkernel
boots (under the opt/gems and opt/bundles directories, respectively), a copy
of the 'bootsync.sh' script (which is, again, under the opt directory in this
project), and the 'rz_mk_init.rb' script itself (which is used by that
bootsync.sh script to start the appropriate Ruby-based services during the
Microkernel boot process).

Copies of the files that appear at the top-level of this project's directory
structure can be found in the /usr/local/bin directory of the Microkernel.  In
addition, the files that appear in the razor_microkernel subdirectory of this
project are all part of the RazorMicrokernel module, and those files are placed
in the /usr/local/lib/ruby/1.8 directory in the Microkernel ISO (ideally this
would be done as part of a "gem install", but we'll leave that work for a later
refactoring of this project.  Finally, there are two MCollective SimpleRPC
agents defined in this project (in the facter-agent and configuration-agent
subdirectories).  The agents from these two folders are place in the
/usr/local/mcollective/plugin/mcollective/agent directories in the Microkernel
ISO (where they should be place if they are to be run by the MCollective
daemon that runs on the Microkernel).  The other two files in those project
subdirectories represent the DDL for each agent and an associated test
SimpleRPC client (in the form of a Ruby script).  These files are meant to
be placed on the Razor Server (or the MCollective Control Node if that is
on a different machine).

It should be noted that this project does not include all of the files that
are needed to build a new instance of the Microkernel ISO.  Instructions for
building a new ISO instance and the files needed to do so maintained elsewhere.
There are also a number of extensions to the standard Tiny Core Linux ISO that
are bundled into the Razor Microkernel which are not included in this project.
Again, instructions for where to obtain these extensions and how to use them
to build your own Microkernel ISO are available elsewhere, and those files are
not included in this project.  We are in the process of determining how best to
keep copies of these additional files so that they are easily accessible from
this project, but there currently is no simple way to do so (since they
typically take the form of large binary objects, and Git doesn't deal too well
with large binary objects).

TO DO Items:

        1. Add ability to deal with multiple registration servers

        2. Add additional actions to the Microkernel Controller; may take
           the form of pluggable extensions that can be downloaded and
           dynamically loaded upon the receipt of an (authorized) command
           in the "checkin" reply...more to come on this