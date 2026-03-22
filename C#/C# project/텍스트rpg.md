1일차
```csharp
using System;

enum STARTSELECT
{
	SELECTTOWN,SELECTBATTLE,NONESELECT,EXIT,
}

class Player
{
	public int AT { get; set;}
	public int HP { get; set;}
	public int MAXHP {get; set;}
	
	public Player()
	{
		AT = 10;
		HP = 100;
		MAXHP = 100;
	}
	
	public void state()
	{
		
	}
}

public class Program
{
	static STARTSELECT StartSelect()
	{
		Console.Clear();
		Console.WriteLine("");
		Console.WriteLine("1.마을");
		Console.WriteLine("2.모험");
		Console.WriteLine("3.종료");
		
		string startInput = Console.ReadLine();
		
		if(startInput == "1")
			return STARTSELECT.SELECTTOWN;
		else if(startInput == "2")
			return STARTSELECT.SELECTBATTLE;
		else if(startInput == "3")
			return STARTSELECT.EXIT;
		else
			return STARTSELECT.NONESELECT;
	}
	
	static void Town()
	{
		while(true)
		{
			Console.Clear();
		
			Console.WriteLine("### 마을 ###");
			Console.WriteLine("1. 회복");
			Console.WriteLine("2. 강화");
			Console.WriteLine("3. 돌아가기");
		
			string townInput = Console.ReadLine();
			switch(townInput)
			{
				case "1":
					break;
				case "2":
					break;
				case "3":
					return;
			}
		}	
	}
	static void Battle()
	{
			
	}
	public static void Main()
	{
		while(true)
		{
			STARTSELECT selected = StartSelect();
			
			switch(selected)
			{
				case STARTSELECT.SELECTTOWN:
					Town();
					break;
				case STARTSELECT.SELECTBATTLE:
					break;
				case STARTSELECT.EXIT:
					return;
			}
		}
	}
}
```
