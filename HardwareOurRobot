package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.NormalizedColorSensor;
import com.qualcomm.robotcore.hardware.NormalizedRGBA;
import com.qualcomm.robotcore.hardware.Servo;
import com.qualcomm.robotcore.hardware.HardwareMap;
import com.qualcomm.robotcore.hardware.SwitchableLight;
import com.qualcomm.robotcore.util.ElapsedTime;


/*
                                     LF       LB       RF       RB

    To Move FORWARD:                ++++     ++++     ----     ----

    To Move BACKWARDS:              ----     ----     ++++     ++++

    To Move LEFT:                   ----     ++++     ----     ++++

    To Move RIGHT:                  ++++     ----     ++++     ----

    To TURN CLOCKWISE:              ++++     ++++     ++++     ++++

    To TURN COUNTERCLOCKWISE:       ----     ----     ----     ----



 */


public class HardwareOurRobot {

    //Wheels
    public DcMotor leftFront;
    public DcMotor leftBack;
    public DcMotor rightFront;
    public DcMotor rightBack;

    //Glyph operators
    public DcMotor liftMotor;
    public Servo clawOfDoomLeft;
    public Servo clawOfDoomRight;

    //Relic operators
    public DcMotor slideMotor;
    public Servo swingLeft;
    public Servo swingRight;


    //Color Sensor stuff
    public Servo colorServo;
    public NormalizedColorSensor Rainbow;


    //Timer
    ElapsedTime driveTime = new ElapsedTime();

    HardwareMap HWMap = null;



//---------------------METHODS------------------------------------------


    //Constructor
    public HardwareOurRobot() {

    }



//---------------------------------INIT--ROBOT------------------------

    public void initializeRobot(HardwareMap hwMap) {

        HWMap = hwMap;

        leftFront = HWMap.dcMotor.get("leftFront");
        leftBack = HWMap.dcMotor.get("leftBack");
        rightFront = HWMap.dcMotor.get("rightFront");
        rightBack = HWMap.dcMotor.get("rightBack");

        liftMotor = HWMap.dcMotor.get("liftMotor");
        clawOfDoomLeft = HWMap.servo.get("clawOfDoomLeft");
        clawOfDoomRight = HWMap.servo.get("clawOfDoomRight");

        slideMotor = HWMap.dcMotor.get("slideMotor");
        swingLeft = HWMap.servo.get("swingLeft");
        swingRight = HWMap.servo.get("swingRight");

        colorServo = HWMap.servo.get("colorServo");

        Rainbow = HWMap.get(NormalizedColorSensor.class, "Rainbow");

        leftFront.setDirection(DcMotor.Direction.REVERSE);
        leftBack.setDirection(DcMotor.Direction.FORWARD);
        rightFront.setDirection(DcMotor.Direction.REVERSE);
        rightBack.setDirection(DcMotor.Direction.FORWARD);

        /*
                SET SERVO INIT VALUES CORRECTLY
         */

        clawOfDoomLeft.setPosition(0.6);
        clawOfDoomRight.setPosition(0.4);
        colorServo.setPosition(0.3);
        swingLeft.setPosition(0.8);
        swingRight.setPosition(0.2);


    }

//-------------------------------INIT--COLOR--SENSOR----------------------------


    public void initializeColorSensor() throws InterruptedException {

        // turn the light on
        if (Rainbow instanceof SwitchableLight) {
            ((SwitchableLight) Rainbow).enableLight(true);
        }


    }


//--------------------------OPEN--AND--CLOSE--CLAWS---------------------------------


    public void openTheCLAWS(){
        clawOfDoomLeft.setPosition(0.8);

        clawOfDoomRight.setPosition(0.2);
    }


    public void  closeTheCLAWS(){
        clawOfDoomLeft.setPosition(1.0);

        clawOfDoomRight.setPosition(0.0);
    }


//-------------------------DRIVE-FORWARD-----------------------------------------------


    public void driveByTime(double powerL, double powerR, double mSec){ //For driving

        driveTime.reset();

        while (driveTime.milliseconds() <= mSec ) {

            leftFront.setPower(powerL);
            leftBack.setPower(powerL);

            rightFront.setPower(powerR);
            rightBack.setPower(powerR);
        }

        leftFront.setPower(0.0);
        leftBack.setPower(0.0);
        rightFront.setPower(0.0);
        rightBack.setPower(0.0);

    }

    //-------------------------DRIVE--MECANUM--FORWARD-----------------------------------------------


    public void driveMecanum(double powerLF, double powerLB, double powerRF, double powerRB, double mSec){ //For driving

        driveTime.reset();

        while (driveTime.milliseconds() <= mSec ) {

            leftFront.setPower(powerLF);
            leftBack.setPower(powerLB);

            rightFront.setPower(powerRF);
            rightBack.setPower(powerRB);
        }

        leftFront.setPower(0.0);
        leftBack.setPower(0.0);
        rightFront.setPower(0.0);
        rightBack.setPower(0.0);

    }


//---------------------------GRAB--AND--LIFT--GLYPH------------------------------------------

    public void grabAndLiftGlyph(){

        openTheCLAWS();

        driveTime.reset();
        while (driveTime.milliseconds() <= 500){

        }

        closeTheCLAWS();

        driveTime.reset();
        while(driveTime.milliseconds() <= 700) {

            liftMotor.setPower(-0.3);
        }

        liftMotor.setPower(0.0);

    }


//--------------------------------------LOWER--GLYPH-----------------------------------------


    public void lowerGlyph(){

        driveTime.reset();
        while(driveTime.milliseconds() <= 700){

            liftMotor.setPower(0.3);

        }

        liftMotor.setPower(0.0);

    }

//-------------------------SENSE--COLOR-----------------------------------------------------


    public String senseColor(String returnValues){

            // Read the sensor
            NormalizedRGBA colors = Rainbow.getNormalizedColors();

            int color = colors.toColor();

            float max = Math.max(Math.max(Math.max(colors.red, colors.green), colors.blue), colors.alpha);
            colors.red /= max;
            colors.green /= max;
            colors.blue /= max;
            color = colors.toColor();




            if ((colors.red > 0.1) && (colors.red > colors.blue)) {

                returnValues = "RED";

            } else if ((colors.blue > 0.1) && (colors.blue > colors.red)) {

                returnValues = "BLUE";

            }
            else {
                returnValues = "NONE";
            }




        return returnValues;

    }


//-------------------------------LOWER--COLOR--SENSOR-----------------------------------------

    public void lowerColorSensor(){

        for(double i = 0.3; i<0.9; i += 0.1) {

            colorServo.setPosition(i);

            driveTime.reset();
            while(driveTime.milliseconds() <= 300){

            }
        }

        colorServo.setPosition(0.97);

    }


}
