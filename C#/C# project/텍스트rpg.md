
```csharp
using System;

enum STARTSELECT
{
	SELECTTOWN,SELECTBATTLE,NONESELECT,EXIT,
}

class Character
{
	public int AT { get; set;}
	public int HP { get; set;}
	public int MAXHP {get; set;}
	public event Action<Character>? Die;
	public string Name {get; set;}
	public Character()
	{
		AT = 10;
		HP = 10;
		MAXHP = 100;
	}
	public void StateRender()
	{
		Console.WriteLine($"[{Name}]====================");
		Console.WriteLine($"AT : {AT}");
		Console.WriteLine($"HP : {HP} / {MAXHP}");
		Console.WriteLine("========================");
	}
	public void Damage(int dam)
	{
		HP-=dam;
		if(HP<0)
		{
			Die?.Invoke(this);
		}
		
	}
}

class Player : Character
{
	
	public void Heal()
	{
		HP=MAXHP;
	}
}

public class Program
{
	static STARTSELECT StartSelect(Player P)
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
	
	static void Town(Player P)
	{
		while(true)
		{
			Console.Clear();
			P.StateRender();
			Console.WriteLine("### 마을 ###");
			Console.WriteLine("1. 회복");
			Console.WriteLine("2. 강화");
			Console.WriteLine("3. 돌아가기");
		
			string townInput = Console.ReadLine();
			switch(townInput)
			{
				case "1":
					P.Heal();
					break;
				case "2":
					break;
				case "3":
					return;
			}
		}	
	}
	static void Battle(Player P)
	{
			
	}
	public static void Main()
	{
		Player NewPlayer = new Player();
		Console.WriteLine("이름은?");
		string name = Console.ReadLine();
		NewPlayer.Name=name;
		
		while(true)
		{
			STARTSELECT selected = StartSelect(NewPlayer);
			
			switch(selected)
			{
				case STARTSELECT.SELECTTOWN:
					Town(NewPlayer);
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
