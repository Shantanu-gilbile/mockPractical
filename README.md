# sparse matrix operations

def Matrix(r, c):
    global a
    a = []
    for i in range(r):
        row = []
        for j in range(c):
            element = int(input(f"Enter elements of matrix {i}{j} : "))
            row.append(element)
        a.append(row)
    return a

def sMatrix(a, r, c):
    sMatrix = []
    tMat = []
    tMat.append(len(a))
    tMat.append(len(a[0]))
    sMatrix.append(tMat)
    for i in range(r):
        for j in range(c):
            temp_list = []
            if a[i][j] != 0:
                temp_list.append(i)
                temp_list.append(j)
                temp_list.append(a[i][j])
                sMatrix.append(temp_list)
    tMat.append(len(sMatrix) - 1)
    return sMatrix

def sparseAddition(mat1, mat2):
    i = 1
    j = 1
    addition = []
    l1 = len(mat1) - 1
    l2 = len(mat2) - 1
    while i <= l1 and j <= l2:
        tempMat = []
        if mat1[i][0] == mat2[j][0]:
            if mat1[i][1] == mat2[j][1]:
                tempMat.append(mat1[i][0])
                tempMat.append(mat1[i][1])
                sum = mat1[i][2] + mat2[j][2]
                tempMat.append(sum)
                addition.append(tempMat)
                i += 1
                j += 1
            else:
                if mat1[i][1] < mat2[j][1]:
                    tempMat.append(mat1[i][0])
                    tempMat.append(mat1[i][1])
                    tempMat.append(mat1[i][2])
                    addition.append(tempMat)
                    i += 1
                else:
                    if mat1[i][1] > mat2[j][1]:
                        tempMat.append(mat2[j][0])
                        tempMat.append(mat2[j][1])
                        tempMat.append(mat2[j][2])
                        addition.append(tempMat)
                        j += 1
        else:
            if mat1[i][0] > mat2[j][0]:
                tempMat.append(mat2[j][0])
                tempMat.append(mat2[j][1])
                tempMat.append(mat2[j][2])
                addition.append(tempMat)
                j += 1
            else:
                if mat1[i][0] < mat2[j][0]:
                    tempMat.append(mat1[i][0])
                    tempMat.append(mat1[i][1])
                    tempMat.append(mat1[i][2])
                    addition.append(tempMat)
                    i += 1
    return addition


def sTransP(sMat):
    res = []
    tempMat = []
    tempMat.append(sMat[0][1])
    tempMat.append(sMat[0][0])
    tempMat.append(sMat[0][2])
    res.append(tempMat)
    for i in range(sMat[0][1]):
        for j in range(1, len(sMat)):
            tempMat1 = []
            if i == sMat[j][1]:
                tempMat1.append(sMat[j][1])
                tempMat1.append(sMat[j][0])
                tempMat1.append(sMat[j][2])
                res.append(tempMat1)

    return res


r1 = int(input("Enter number of rows: "))
c1 = int(input("Enter number of columns: "))
mat1 = Matrix(r1, c1)

r2 = int(input("Enter number of rows: "))
c2 = int(input("Enter number of columns: "))
mat2 = Matrix(r2, c2)

sMat1 = sMatrix(mat1, r1, c1)
sMat2 = sMatrix(mat2, r2, c2)

print("sparse Matrix 1:")
print(sMatrix(mat1, r1, c1))

print("sparse Matrix 2: ")
print(sMatrix(mat2, r2, c2))
print("Addition of two Sparse matrix is : ")
print(sparseAddition(sMat1, sMat2))

print("Transepose of Matrix 1 is: ")
print(sTransP(sMat1))
print("Transepose of Matrix 2 is: ")
print(sTransP(sMat2))


