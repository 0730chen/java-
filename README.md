# java-
package workspace01;
//数组的操作 一维二维数组的初始化
public class Exmaple08 {
	char[] cNum = {'1','2','3','4','5','6','7','8','9','0'};
	char[] cStr = {'a','b','c','d','e','f','g','h',
			       'i','j','k','l','m','n','o','p',
			       'q','r','s','t','u','v','w','x','y','z'};
	int[] iMonth = {31,28,31,30,31,30,31,31,30,31,30,31};
	String[] sMail = {"@","."};
	//方法说明 检验电子邮件 输入电子邮件地址 返回类型为boolean类型
	public boolean isMail(String sPara) {//被检验的电子邮件字符
		for(int i =0;i<sMail.length;i++) {
			if(sPara.indexOf(sMail[i])==-1) {
				return false;
			}
		}
		return true;
	}
	
	public boolean isNumber(String sPara) {//判断是否是数字 全部都是数字则为TRUE
		int ipLength = sPara.length();
		for(int i = 0;i<ipLength;i++) {
			char cTemp = sPara.charAt(i);
			boolean bTemp = false;
			for(int j =0;j<cNum.length;j++) {
				if(cTemp==cNum[j]) {
					bTemp=true;
					break;
				}
			}
			if(!bTemp) {return false;}
		}
		return true;
	}
	//判断是否都为英文字母
	public boolean isString(String sPara) {
		int ipLength = sPara.length();
		for(int i =0;i<ipLength;i++) {
			char cTemp = sPara.charAt(i);
			boolean bTemp = false;
			for(int j=0;j<cStr.length;j++) {
				if(cTemp==cStr[j]) {
					bTemp = true;
					break;
				}
			}
			if(!bTemp) {return false;}
		}
		return true;
	}
	//判断是否是闰年
	public boolean chickDay(int iPara) {
		return iPara%100==0 && iPara%4==0;
	}
	//检查日期格式是否正确
	//0则正确 -1则返回月份或者日期不对 -2 年月日格式不对
	public int chickData(String sPara) {
		boolean bTemp = false;
		//输入长度不对
		if(sPara.length()!=10) {return -2;}
		//获取年
		String sYear = sPara.substring(0, 4);
		//判断是否是数字
		if(!isNumber(sYear)) {return -2;}
		//获取月份
		String sMonth = sPara.substring(5,7);
		if(!isNumber(sMonth)) {return -2;}
		//获取日期
		String sDay = sPara.substring(8,10);
		//判断日期是否是数字
		if(!isNumber(sDay)) {return -2;}
		//将年月日转变成数字
		int iYear = Integer.parseInt(sYear);
		int iMon = Integer.parseInt(sMonth);
		int iDay = Integer.parseInt(sDay);
		if(iMon>12) {return -1;}
		//闰年二月处理
		if(iMon==2&&chickDay(iYear)) {
			if(iDay>29) {return -2;}
		}else {
			if(iDay>iMonth[iMon-1]) {return -1;}
		}
		return 0;
	}
	//主方法测试 输入参数 返回类型
	public static void main(String args[]) {
		Exmaple08 mA = new Exmaple08();
		boolean bMail = mA.isMail("tom@163.com");
		//是否是邮箱地址
		System.out.println("1 bMail is"+bMail );
		bMail = mA.isMail("tom@163com");
		System.out.println("2 bMail is "+bMail);
		//检查是否是数字
		boolean bIsnum = mA.isNumber("1234");
		System.out.println("1 bIsnum is"+bIsnum);
		bIsnum = mA.isNumber("123456r");
		System.out.println("2 bIsnum is"+bIsnum );
		//检测是否是英文字符
		boolean bIsstr = mA.isString("abcdsa");
		System.out.println("1 bIsstr is "+ bIsstr);
		bIsstr = mA.isString("1sdd54");
		System.out.println("2 bIsstr is "+bIsstr);
		//检测日期
		int bIsTime = mA.chickData("2003-12-98");
		System.out.println("1 bIsTime ="+bIsTime);
		bIsTime = mA.chickData("2004-111-10");
		System.out.println("2 bIsTime ="+bIsTime);
		bIsTime = mA.chickData("2003-10-08");
		System.out.println("3 bIsTime = "+bIsTime);
		bIsTime = mA.chickData("2000-02-30");
		System.out.println("4 bIsTime = "+ bIsTime);
	}

}
