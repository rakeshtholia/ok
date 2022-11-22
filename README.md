# AS_03
    pragma solidity 0.4.25;

    contract Bank {
    int bal;
    constructor() public{
        bal=1;
    }

    function InputAndOutputParameters(int inputParam1) {
       bal =  inputParam1;
    }


    function getBalance() view public returns(int)
    {
        return bal;
    }
    function withdraw(int amt) public
    {
        if(bal<amt){
            revert("amount is not enough for withdrawl");
        }
        bal = bal -amt;
    }
    function deposit(int amt) public
    {
        bal = bal + amt;
    }

}


# As_04
    pragma solidity 0.4.25;
    contract StudentRegister{
        address public owner;
        mapping (uint256=>student)students;
        constructor() public {
            owner=msg.sender;
        }
        modifier onlyOwner {
            require(msg.sender==owner);
            _;
        }
        struct student{
            uint256 studentId;
            string  name;
            string course;
            uint256 mark1;
            uint256 mark2;
            uint256 mark3;
            uint256 totalMarks;
            uint256 percentage;
            bool isExist;   
        }
        function() public payable{
                revert("ha.. ha... Fraud Not Possible,student details already registered and cannot be altered");
        }
        function register(uint256 studentId,string memory name,string memory course,uint256 mark1,uint256 mark2,uint256 mark3) public onlyOwner {
                require(students[studentId].isExist==false,"ha.. ha... Fraud Not Possible,student details already registered and cannot be altered");
                uint256 totalMarks;
                uint256 percentage;
                totalMarks=(mark1+mark2+mark3);
                percentage=(totalMarks/3);       
                students[studentId]=student(studentId,name,course,mark1,mark2,mark3,totalMarks,percentage,true);
        }       
        function getStudentDetails(uint256 studentId) public view returns (uint256,string memory,string memory,uint256,uint256){
            return(students[studentId].studentId,students[studentId].name,students[studentId].course,students[studentId].totalMarks,students[studentId].percentage);
        }
    }
