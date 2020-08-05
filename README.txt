WebEx Meeting activity (mod_webexactivity)

Maintainer  Eric Merrill (merrill@oakland.edu)
Copyright   2016 Oakland University
License     GNU GPL v3 or later http://www.gnu.org/copyleft/gpl.html
=========

A Moodle activity module for Cisco WebEx.

Disclaimer
==========
WebEx, Cisco WebEx, Cisco and the WebEx Ball logo are Registered Trademarks of Cisco.
This module is in no way affiliated with, endorsed by, or approved by Cisco. 
As specified in GNU GPL v3, this software is provided as is, without any warranty.


Current Limitations
===================
As this software is in beta, you should see the Limitations and Bugs list at:
https://github.com/merrill-oakland/moodle-mod_webexactivity/wiki/Limitations-and-Bugs

Highlights for this release:
- If you host one meeting type (like Meeting Center), and then go to try and host a meeting of a different type (Training Center)
  you may get an error. Workaround: Go to the WebEx site and click "Log out". Then try again.
- Backup and restore does not work.
- When a Moodle user is used to create or host a meeting, a new WebEx user is created for them, with the prefix setting prepended to
  the username. If the email address is already taken, the user will be redirected to a field to enter their WebEx password. A
  workaround for this is to change the users existing email address in WebEx from something like user1@example.com to
  user1+webex@example.com. Everything between the + and the @ is ignored by email systems.
- Only Meeting Center and Training Center are currently supported.


Documentation
=============
For Requirements, Installation information, and the Change Log, please visit:
https://github.com/merrill-oakland/moodle-mod_webexactivity/wiki


ไปที่โฟลเดอร์ classes -> local -> type -> base -> meeting.php
อยู่ที่ บรรทัด 1041 

define('LINE_API',"https://notify-api.line.me/api/notify");

                $token = "ipBZ4pwuPUpAJoPgyVFXUtQ5AGp7v9H5P4B0Of9EKGu"; //ใส่Token ที่copy เอาไว้
                $str = "Hello"; //ข้อความที่ต้องการส่ง สูงสุด 1000 ตัวอักษร
                $queryData = array('message' => $this->name.' '.$this->course.' '.strtotime($this->starttime));
                $queryData = http_build_query($queryData,'','&');
                $headerOptions = array( 
                        'http'=>array(
                            'method'=>'POST',
                            'header'=> "Content-Type: application/x-www-form-urlencoded\r\n"
                                    ."Authorization: Bearer ".$token."\r\n"
                                    ."Content-Length: ".strlen($queryData)."\r\n",
                            'content' => $queryData
                        ),
                );
                $context = stream_context_create($headerOptions);
                $result = file_get_contents(LINE_API,FALSE,$context);
                $res = json_decode($result);
                print_r($res);
