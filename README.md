# Parking-Area-Management
This is java Program manages the vehicles

class ParkingArea{
          private String name;
          private int parkingSlots;
          private ParkingGate parkingGate;
          final int MAX_PARKING_SLOTS = 9; 
    
          ParkingArea(ParkingGate parkingGate)
          {
                  name="MIT Parking";
                  parkingSlots=0;
                  this.parkingGate=parkingGate;
          }

          int getParkingSlots(){
                   return parkingSlots;
           }

           void vehicleIn(Vehicle vehicle){
                  System.out.println("\nVehicle In :"+vehicle.getNumber());

                  if(parkingSlots < MAX_PARKING_SLOTS){
                  parkingGate.open(this,vehicle,'I');
                          parkingSlots++;
                 }else{
                 System.out.println("Parking Space is full");
            }
    }

            void vehicleOut(Vehicle vehicle){
            System.out.println("\nVehicle Out :" + vehicle.getNumber());
            if(parkingSlots>0)
           {
             
             parkingGate.open(this,vehicle,'O');
                      parkingSlots--;
          }else{  
             System.out.println("Parking Space is Empty");
         }
    }
 }
  
 
   class ParkingGate{
                  private boolean state;
                  int[] vehicleRecord = new int[9];
                  ParkingGate(boolean state)
                  {
                          this.state=state;
                  }void open(ParkingArea area,Vehicle vehicle,char openFor){
        if(openFor=='I'){
            vehicleRecord[area.getParkingSlots()]=vehicle.getNumber();
        }else if(openFor=='O'){
            int[] temp = new int[9];
            int i=0;
            for(int number:vehicleRecord){
                if(number==vehicle.getNumber())
                    temp[i]=0;
                else
                    temp[i]=number;
                     i++;
                 }
                      i=0;
            for(int num:temp){
                vehicleRecord[i]=num;
                i++;
            }
        }
   }

    
                        void close(){
               System.out.println("Parking gate closes.");  
        }
  }
    
 class Vehicle {
           int number;
           String color;
           String company;

          Vehicle(int number,String color,String company){
                  this.number=number;
                  this.color=color;
                  this.company=company;
           }

           int getNumber(){
                return number;
           }
           void display(){
                 System.out.println("Number :"+ number);
                 System.out.println("Color : "+color);
                 System.out.println("company :"+company);
           }
           
   }
   
   class Car extends Vehicle{
                  int occupancy;
                 
          Car(int number,String color,String company,int occupancy){
                   super(number,color,company);
                   this.occupancy=occupancy;
          }   

          void display(){
                  System.out.println("Type      : Car");
                  System.out.println("Number :"+ number);
                  System.out.println("Color : "+color);
                  System.out.println("company :"+company);
                  System.out.println("Occupancy :"+occupancy);
           }
   }
   class Bus extends Vehicle{
                   int passangerCapacity;
           
                  Bus(int number,String color,String company,int passangerCapacity){
                          super(number,color,company);
                          this.passangerCapacity=passangerCapacity;
                  }
                  void display(){
                           System.out.println("Type      : Bus");
                           System.out.println("Number :"+ number);
                           System.out.println("Color : "+color);
                           System.out.println("company :"+company);
                           System.out.println("Passanger Capacity :"+passangerCapacity);
                  }
       }
  
  class Truck extends Vehicle{
                  int loadCapacity;

                  Truck(int number,String color,String company,int loadCapacity){
                            super(number,color,company);
                            this.loadCapacity=loadCapacity;
                  }
                  void display(){
                            System.out.println("Type      : Truck"); 
                            System.out.println("Number :"+ number);
                            System.out.println("Color : "+color);
                            System.out.println("company :"+company);
                            System.out.println("Load Capacity :"+loadCapacity);
                  }
       }
  class ParkingDemo{
        public static void main(String args[]){
             ParkingGate gate =new ParkingGate(false);
             ParkingArea area = new ParkingArea(gate);
             Car  car1 = new Car(1234,"White","TATA",4);
             Bus  bus1=new Bus(1235,"Red","Volvo",50);
             Truck truck1=new Truck(3456,"Black","Mahindra",1000);
              area.vehicleIn(car1);
              area.vehicleIn(bus1);
              area.vehicleIn(truck1);

              System.out.println("Parking Slots Occupied: "+area.getParkingSlots());
              int slot=0;
              for(int number : gate.vehicleRecord){
                     slot++;
                     System.out.println("Slot"+slot+":"+number);
              }
              area.vehicleOut(truck1);
              area.vehicleOut(bus1);
              
              System.out.println("Parking Slots Occupied: "+area.getParkingSlots());
		slot=0;
		for(int number: gate.vehicleRecord)
		{	
			slot++;
			System.out.println("Slot "+slot+": "+number);
		}


	}
}
