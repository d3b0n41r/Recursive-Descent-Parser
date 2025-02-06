using System;

namespace ConsoleApp2
{
    internal class Program 
    {
        static void Main(string[] args)
        {
            string expression = Console.ReadLine();
            int i = 0;
            unit root = parseUnit(expression, ref i);
            root.writeTree(root, "");
            Console.ReadLine();
        }
        public static unit parseUnit(string expr, ref int position)
        {
            if (expr[position] == '(')
            {
                position++;
                expression unitExpr = parseExpr(expr, ref position);
                position++;
                return new unit(unitExpr, null);
            }
            string op = parseIdentifier(expr, ref position);
            return new unit(null, op);
        }
        public static expression parseExpr(string expr, ref int position)
        {
            unit leftUnit = parseUnit(expr, ref position);
            char op = expr[position];
            position++;
            unit rightUnit = parseUnit(expr, ref position);
            return new expression(leftUnit, op, rightUnit);
        }
        public static string parseIdentifier(string expr, ref int position)
        {
            string subS = "";
            int length = 0;
            for (int i = position; i < expr.Length; i++)
            {
                if (!Char.IsLetter(expr[i]))
                {
                    length = i - position;
                    subS = expr.Substring(position, length);
                    position = i;
                    break;
                }
            }
            return subS;
        }
    }
    class unit 
    {
        public expression expression;
        public string identifier;
        public unit(expression expression, string identifier)
        {
            this.expression = expression;
            this.identifier = identifier;
        }
        public void writeTree(unit root, string prefix)
        {
            if (root.expression != null)
            {
                Console.WriteLine(prefix + "+- " + root.expression.op);
                if (root.expression.left != null) writeTree(root.expression.left, prefix + "|  ");
                if (root.expression.right != null) writeTree(root.expression.right, prefix + "|  ");
            }
            else Console.WriteLine(prefix + "+- " + root.identifier);
        }
    }
    class expression
    {
        public unit left;
        public char op;
        public unit right;
        public expression(unit left, char op, unit right)
        {
            this.left = left;
            this.op = op;
            this.right = right;
        }
    }
}
