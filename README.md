# medimage-addon-ehr-soaptest
A testing configuration against a sample AtomJump messaging forum page.

# MedImage Server Setup

1. Open port 80 on the server holding the MedImage Server, or ideally a secure port, 443.
2. Change the C:\MedImage\config.json, listenPort figure to the port above, and restart the MedImage service
3. Change the target photo folder in MedImage settings to C:\MedImage\public\image\photos, to make the photos publicly visible

# EHR Connector Setup

Request Style: Use JSON

Then under ‘Show Endpoint SOAP/JSON Options’

Example check connection endpoint:
`https://atomjump.com/api/plugins/inserter/index.php`

But where you should point towards your own installation of AtomJump rather than the atomjump server's version. i.e.
`https://yourserver.com/atomjump-messaging-path/plugins/inserter/index.php`

Example Insert attachment endpoint:
E.g.
`https://atomjump.com/api/plugins/inserter/index.php?forum=ajps_changeme-demo&msg=Patient:+[patientID].++Photo:+[photoname]+http%3A%2F%2F35.244.84.80%2Fimages%2Fphotos%2F[patientID]%2F[photoname].jpg&code=249856hhgf-2ytyghhvdjnsetkj`

But remember you should use the same path to your installation of AtomJump
`https://yourserver.com/atomjump-messaging-path/plugins/inserter/index.php`
at the start of this attachment endpoint.

A 'URL decoded' version of the msg parameter, above, is:
`Patient:+[patientID].++Photo:+[photoname]+http://35.244.84.80/images/photos/[patientID]/[photoname].jpg&code=249856hhgf-2ytyghhvdjnsetkj`

To explain this: the first section is the text to appear in the message (and [patientID] gets written over with the ID itself, as does [photoname] with the photo’s name). The URL after http is the web address of the Windows server holding the EHR Connector, and the photos are served up by the MedImage Server on that server, which is accessible remotely.

Important Note: the whole system should ideally be on an intranet, to ensure security over access to the photos. Our demo is not secure, and the photo security is purely “security via obscurity”.


