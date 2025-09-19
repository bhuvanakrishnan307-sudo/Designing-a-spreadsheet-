# Designing-a-spreadsheet-
Designing a spreadsheet using Python 
class Spreadsheet(object):
    def __init__(self, rows):
        self.cells = {}  # Dictionary to store cell values

    def setCell(self, cell, value):
        self.cells[cell] = value

    def resetCell(self, cell):
        self.cells[cell] = 0

    def getValue(self, formula):
        # Formula is of the format "=X+Y"
        formula = formula[1:]  # Remove '='
        part1, part2 = formula.split('+')

        def get_val(x):
            if x.isdigit():  # If it's a number
                return int(x)
            return self.cells.get(x, 0)  # If it's a cell reference

        return get_val(part1) + get_val(part2)


if __name__ == "__main__":
    commands = ["Spreadsheet", "getValue", "setCell", "getValue",
                "setCell", "getValue", "resetCell", "getValue"]
    params = [[3], ["=5+7"], ["A1", 10], ["=A1+6"],
              ["B2", 15], ["=A1+B2"], ["A1"], ["=A1+B2"]]

    output = []
    for i, cmd in enumerate(commands):
        if cmd == "Spreadsheet":
            obj = Spreadsheet(*params[i])
            output.append(None)
        elif cmd == "setCell":
            obj.setCell(*params[i])
            output.append(None)
        elif cmd == "resetCell":
            obj.resetCell(*params[i])
            output.append(None)
        elif cmd == "getValue":
            res = obj.getValue(*params[i])
            output.append(res)

    print(output)
