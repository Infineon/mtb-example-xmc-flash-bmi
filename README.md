# XMC&trade; MCU: Flash BMI

This example demonstrates how boot mode index (BMI) can be used to configure a customized boot sequence on XMC4000 series of devices.

**Warning:** This code example involves programming the user configuration blocks (UCB), which can be programmed only a limited number of times. See the [Design and implementation](#design-and-implementation) section before proceeding with this code example.

## Requirements

- [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) v3.0 or later (tested with v3.3)
- [SEGGER J-Link software](https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack)
- Programming language: C
- Associated parts: [XMC™ 4000 series MCU](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/32-bit-xmc4000-industrial-microcontroller-arm-cortex-m4/) parts

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm® embedded compiler v11.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`

## Supported kits (make variable 'TARGET')

- [XMC4700 relax kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc47_relax_v1/) (`KIT_XMC47_RELAX_V1`) - Default value of `TARGET`
- [XMC4200 Platform2GO XTREME Kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc_plt2go_xmc4200/) (`KIT_XMC_PLT2GO_XMC4200`)
- [XMC4300 relax EtherCAT Kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc43_relax_ecat_v1/) (`KIT_XMC43_RELAX_ECAT_V1`)
- [XMC4400 Platform2GO XTREME Kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc_plt2go_xmc4400/) (`KIT_XMC_PLT2GO_XMC4400`)
- [XMC4800 relax EtherCAT kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc48_relax_ecat_v1/) (`KIT_XMC48_RELAX_ECAT_V1`)

## Hardware setup

This example uses the board's default configuration. See the kit user guide to ensure that the board is configured correctly.

## Software setup

Install a terminal emulator if you don't have one. Instructions in this document use [Tera Term](https://teratermproject.github.io/index-en.html).

This example requires no additional software or tools.

## Using the code example

### Create the project

The ModusToolbox&trade; tools package provides the Project Creator as both a GUI tool and a command line tool.

<details><summary><b>Use Project Creator GUI</b></summary>

1. Open the Project Creator GUI tool.

   There are several ways to do this, including launching it from the dashboard or from inside the Eclipse IDE. For more details, see the [Project Creator user guide](https://www.infineon.com/ModusToolboxProjectCreator) (locally available at *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/docs/project-creator.pdf*).

2. On the **Choose Board Support Package (BSP)** page, select a kit supported by this code example. See [Supported kits](#supported-kits-make-variable-target).

   > **Note:** To use this code example for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. On the **Select Application** page:

   a. Select the **Applications(s) Root Path** and the **Target IDE**.

   > **Note:** Depending on how you open the Project Creator tool, these fields may be pre-selected for you.

   b.	Select this code example from the list by enabling its check box.

   > **Note:** You can narrow the list of displayed examples by typing in the filter box.

   c. (Optional) Change the suggested **New Application Name** and **New BSP Name**.

   d. Click **Create** to complete the application creation process.

</details>

<details><summary><b>Use Project Creator CLI</b></summary>

The 'project-creator-cli' tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the 'project-creator-cli' tool. On Windows, use the command-line 'modus-shell' program provided in the ModusToolbox&trade; installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; tools. You can access it by typing "modus-shell" in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The following example clones the "[Flash BMI](https://github.com/Infineon/mtb-example-xmc-flash-bmi)" application with the desired name "MyFlashBMI" configured for the *KIT_XMC47_RELAX_V1* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id KIT_XMC47_RELAX_V1 --app-id mtb-example-xmc-flash-bmi --user-app-name MyFlashBMI --target-dir "C:/mtb_projects"
   ```

<mark>Update the above paragraph and commands to match your CE.

The 'project-creator-cli' tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the <id> field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the <id> field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

> **Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; tools package user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at {ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf).

</details>



### Open the project

After the project has been created, you can open it in your preferred development environment.


<details><summary><b>Eclipse IDE</b></summary>

If you opened the Project Creator tool from the included Eclipse IDE, the project will open in Eclipse automatically.

For more details, see the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>


<details><summary><b>Visual Studio (VS) Code</b></summary>

Launch VS Code manually, and then open the generated *{project-name}.code-workspace* file located in the project directory.

For more details, see the [Visual Studio Code for ModusToolbox&trade; user guide](https://www.infineon.com/MTBVSCodeUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_vscode_user_guide.pdf*).

</details>


<details><summary><b>Keil µVision</b></summary>

Double-click the generated *{project-name}.cprj* file to launch the Keil µVision IDE.

For more details, see the [Keil µVision for ModusToolbox&trade; user guide](https://www.infineon.com/MTBuVisionUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_uvision_user_guide.pdf*).

</details>


<details><summary><b>IAR Embedded Workbench</b></summary>

Open IAR Embedded Workbench manually, and create a new project. Then select the generated *{project-name}.ipcf* file located in the project directory.

For more details, see the [IAR Embedded Workbench for ModusToolbox&trade; user guide](https://www.infineon.com/MTBIARUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_iar_user_guide.pdf*).

</details>


<details><summary><b>Command line</b></summary>

If you prefer to use the CLI, open the appropriate terminal, and navigate to the project directory. On Windows, use the command-line 'modus-shell' program; on Linux and macOS, you can use any terminal application. From there, you can run various `make` commands.

For more details, see the [ModusToolbox&trade; tools package user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>



## Operation

1. Connect the board to your PC using a micro-USB cable through the debug USB connector.

2. Open a terminal program and select the *JLINK CDC UART COM port*. Configure the terminal with a baud rate of 115200, data bits of 8, stop bit of 1, and with parity and flow control set to none.

3. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE</b></summary>

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (JLink)**.
   </details>
   
   <details><summary><b>In other IDEs</b></summary>

   Follow the instructions in your preferred IDE.
   </details>


   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The default toolchain is specified in the application's Makefile but you can override this value manually:
      ```
      make program TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TOOLCHAIN=GCC_ARM
      ```
   </details>


4. Once programmed, open your serial terminal software. You should see the shell application displayed as shown follows:

   **Figure 1. Shell application**

   ![](images/shell.png)

5. Do the following to install flash read protection using the shell application:

   1. Type `status` to get the status of the BMI installation and UCB program count:

      ```
      >> status
      ```

      **Figure 2. BMI installation status**

      ![](images/status.png)

   2. Type `install` to install the BMI configuration into UCB2.

      The device will reset after this command for the changes to take effect.

      For example:

      ```
      >> install
      ```

      **Figure 3. Install BMI configuration**

      ![](images/install.png)

   3. Check the status to see if the BMI installation was successful. The UCB program count will also be displayed.

      ```
      >> status
      ```

      **Figure 4. BMI installation status**

      ![](images/bmi_status.png)

   4. Type `usb` to read the USB serial number loaded into DSRAM1:

      ```
      >> usb
      ```

      **Figure 5. USB serial number**

      ![](images/usb.png)

   5. Type `mac` to read the MAC address loaded into DSRAM1:

      ```
      >> mac
      ```

      **Figure 6. MAC address**

      ![](images/mac.png)

   6. Type `ipv4` to read the IPv4 address (LSB) loaded into DSRAM1:

      ```
      >> ipv4
      ```

      **Figure 7. IPV4 address (LSB)**

      ![](images/ip.png)


**Note:** If the kit is reset or power cycled when running this example, the program will start in normal mode because of the state of the TMS/TCK pins even if the BMI has been installed previously. Therefore, the BMI installation status will be seen as invalid. Install the BMI string again if this happens.

<br>

## Debugging


You can debug the example to step through the code.


<details><summary><b>In Eclipse IDE</b></summary>

Use the **\<Application Name> Debug (JLink)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).


</details>


<details><summary><b>In other IDEs</b></summary>

Follow the instructions in your preferred IDE.
</details>



## Design and implementation

XMC4000 family of devices supports several boot modes such as the following:

- Normal boot mode
- Alternative boot mode
- Fallback ABM
- PSRAM boot mode
- ASC BSL boot mode
- CAN BSL boot mode
- Boot mode index (BMI)

BMI mode allows you to customize the boot sequence using a BMI string. The BMI string is written into the **user configuration block 2 (UCB) Page1**. This defines the set of activities to be performed on startup.

Upon reset, the startup software copies the BMI string into a 64-byte location in DSRAM1. These 64 bytes can be used to store the MAC address, USB serial number, and the IP address.

In this code example, UCB2 is programmed with a BMI string that copies the MAC address, USB serial number, and the IP address to DSRAM1 before going into normal boot Mode.

A custom linker script specifies the additional size required to store the BMI string in the DSRAM region. It is located in the *CUSTOM_DESIGN_MODUS* folder of the respective kits. The Makefile variable `LINKER_SCRIPT` specifies the custom linker script to be selected corresponding to the `TARGET` being used.

**Figure 8. Firmware flow diagram**

![](images/block_diagram.png)

The code example uses a shell application to take input commands from the user to perform five different operations:

Command | Description
------- | -----------------
`install` | Installs the BMI string into UCB2
`usb` | Retrieves USB serial number from DSRAM1
`mac` | Retrieves the MAC address from DSRAM1
`ipv4` | Retrieves the IPv4 address from DSRAM1
`status` | Displays the BMI installation status

<br>

**Warning:** The BMI String is modified by erasing and programming the UCB2. **The erase and re-program of the UCBs can be performed up to four times. Exceeding this limit may make the device unusable.**


## Resources and settings

The code example uses a custom *design.modus* file because it uses the **universal serial interface channel (USIC)** block to implement the shell application. The following settings were modified in the default *design.modus* file.

**Figure 9. USIC (UART) settings**

![](images/design_modus.png)

<br>

**Figure 10. UART Rx settings**

![](images/rx.png)

<br>

**Figure 11. UART Tx settings**

![](images/tx.png)

## Related resources
Resources | Links
----------|--------
Kit guides  | [XMC4200 Platform2GO XTREME kit](https://www.infineon.com/dgdl/Infineon-XMC4200_Platform2Go-UserManual-v01_00-EN.pdf?fileId=5546d4626f229553016f8fca76c12c96) <br> [XMC4300 relax EtherCAT kit](https://www.infineon.com/dgdl/Infineon-XMC4300_Relax_Kit-UM-v01_00-EN.pdf?fileId=5546d46269e1c019016a78da2104554d) <br> [XMC4400 Platform2GO XTREME kit](https://www.infineon.com/dgdl/Infineon-XMC4400_Platform2Go-UserManual-v01_00-EN.pdf?fileId=5546d4626f229553016f8fc159482c94) <br> [XMC4500 relax kit](https://www.infineon.com/dgdl/Board_Users_Manual_XMC4500_Relax_Kit-V1_R1.2_released.pdf?fileId=db3a30433acf32c9013adf6b97b112f9) <br> [XMC4700/XMC4800 relax kit series-V1](https://www.infineon.com/dgdl/Infineon-Board_User_Manual_XMC4700_XMC4800_Relax_Kit_Series-UM-v01_02-EN.pdf?fileId=5546d46250cc1fdf01513f8e052d07fc)
| Code examples on Github | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software)
 Device documentation  | [XMC4000 family datasheets](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/32-bit-xmc4000-industrial-microcontroller-arm-cortex-m4/#document-group-myInfineon-49) <br> [XMC4000 family technical reference manuals](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/32-bit-xmc4000-industrial-microcontroller-arm-cortex-m4/#document-group-myInfineon-44)
Development kits | [XMC&trade; MCU eval boards](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/#boards)
Libraries on GitHub | [mtb-xmclib-cat3](https://github.com/Infineon/mtb-xmclib-cat3) – XMC&trade; MCU peripheral library (XMCLib) and docs
Tools | [Eclipse IDE for ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices.         |

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

For XMC&trade; MCU devices, see [32-bit XMC™ industrial microcontroller based on Arm® Cortex®-M](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/).

## Document history

Document title: *CE232718* - *XMC&trade; MCU: Flash BMI*

| Version | Description of change |
| ------- | --------------------- |
| 1.0.0   | New code example      |
| 1.1.0   | Added support for new kits |
| 2.0.0   | Updated to support ModusToolbox&trade; software v3.0. <br> This CE is not backward-compatible with previous versions of ModusToolbox™ software |
| 2.0.1   | Updated README        |
| 2.1.0   | Updated code to use retarget-io-cat3 middleware for shell operations |
------

All other trademarks or registered trademarks referenced herein are the property of their respective owners.

© 2024 Infineon Technologies AG

All Rights Reserved.

### Legal disclaimer

The information given in this document shall in no event be regarded as a guarantee of conditions or characteristics. With respect to any examples or hints given herein, any typical values stated herein and/or any information regarding the application of the device, Infineon Technologies hereby disclaims any and all warranties and liabilities of any kind, including without limitation, warranties of non-infringement of intellectual property rights of any third party.

### Information

For further information on technology, delivery terms and conditions and prices, please contact the nearest Infineon Technologies Office (www.infineon.com).

### Warnings

Due to technical requirements, components may contain dangerous substances. For information on the types in question, please contact the nearest Infineon Technologies Office.

Infineon Technologies components may be used in life-support devices or systems only with the express written approval of Infineon Technologies, if a failure of such components can reasonably be expected to cause the failure of that life-support device or system or to affect the safety or effectiveness of that device or system. Life support devices or systems are intended to be implanted in the human body or to support and/or maintain and sustain and/or protect human life. If they fail, it is reasonable to assume that the health of the user or other persons may be endangered.

-------------------------------------------------------------------------------
