using System;

namespace ConsoleApp2
{
    internal class Program
    {
        static void Main(string[] args)
        {
            string expression = Console.ReadLine();
            int i = 0;
            unit root = parseUnit(expression, ref i, false);
            root.writeTree(root, "");
            Console.ReadLine();
        }
        public static unit parseUnit(string expr, ref int position, bool nextOperatorNot)
        {
            bool nextOperandNot = false;
            if(expr[position] == '!')
            {
                if (expr[position + 1] == '(')
                {
                    nextOperatorNot = true;
                    position++;
                }
                else
                {
                    position++;
                    nextOperandNot = true;
                }
            }
            if (expr[position] == '(')
            {
                position++;
                expression unitExpr = parseExpr(expr, ref position, nextOperatorNot);
                position++;
                return new unit(unitExpr, null);
            }
            string op = nextOperandNot ? ("!" + parseIdentifier(expr, ref position)) : parseIdentifier(expr, ref position);
            return new unit(null, op);
        }
        public static expression parseExpr(string expr, ref int position, bool nextNot)
        {
            unit leftUnit = parseUnit(expr, ref position, nextNot);
            string op = nextNot ? ("!" + expr[position]) : expr[position].ToString();
            nextNot = false;
            position++;
            unit rightUnit = parseUnit(expr, ref position, nextNot);
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
        public string op;
        public unit right;
        public expression(unit left, string op, unit right)
        {
            this.left = left;
            this.op = op;
            this.right = right;
        }
    }
}
