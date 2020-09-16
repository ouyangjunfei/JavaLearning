# Scanner输入注意事项

近期在看牛客和赛码的编程题时，注意到有关Java输入方面的问题。

如果题目提供数据全部为数字且有多组，使用`while`进行判断是否结束，使用`nextInt()`读取即可，其会自动跳过任意数量的空格和回车换行，正如代码示例

```Java
    //计算数字a与b之和
    Scanner in = new Scanner(System.in);
    int a,b;
    while (in.hasNextInt()) {
        a = in.nextInt();
        b = in.nextInt();
        System.out.println(a + "---" + b);
    }
```

接下来一种情况非常容易出问题，即题目要求第一行输入某数字`n`，接下来是`n`行字符串内容。

不少同学会觉得自己明明代码写对了，却没有AC。

原因在于`nextInt()`**不会**吃掉**回车换行符**，所以数字后面的回车换行符被**本应该**读取字符串内容的下一个变量读取，导致读入内容出错。

正确的处理办法是在`nextInt()`后加一行不赋值给变量的`nextLine()`，见如下示例代码。

```Java
    //读入一行数字和若干行字符串
    Scanner in = new Scanner(System.in);
    int a;
    String b;
    while (in.hasNext()) {
        a = in.nextInt();
        in.nextLine();  //******关键，吃掉数字后的回车换行符
        b = in.nextLine();
        System.out.println(a + "---" + b);
    }
```