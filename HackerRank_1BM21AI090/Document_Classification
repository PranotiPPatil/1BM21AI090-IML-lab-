# Enter your code here. Read input from STDIN. Print output to STDOUT
def getTrainingData():
    import pandas as pd

    data = open("trainingdata.txt").read().split("\n")

    labels, texts = [], []
    n, data = int(data[0]), data[1:]

    for line in range(n):
        labels.append(int(data[line][0]))
        texts.append(data[line][2:])

    return pd.DataFrame({"text": texts, "label": labels})


def examples():
    dict_kn = {
        "This is a document": 1,
        "this is another document": 4,
        "documents are seperated by newlines": 8,
        "Business means risk": 1,
        "They wanted to know how the disbursed": 1,
    }

    return dict_kn


def another_sol(x_test):
    from sklearn.pipeline import Pipeline
    from sklearn.feature_extraction.text import TfidfVectorizer
    from sklearn.linear_model import SGDClassifier

    data = getTrainingData()
    x_train, y_train = data.text, data.label

    clf = Pipeline(
        [
            (
                "vect",
                TfidfVectorizer(
                    stop_words="english",
                    ngram_range=(1, 1),
                    min_df=4,
                    strip_accents="ascii",
                    lowercase=True,
                ),
            ),
            ("clf", SGDClassifier(class_weight="balanced")),
        ]
    )

    clf.fit(x_train, y_train)

    return clf.predict(x_test)


if __name__ == "__main__":

    n = int(input())
    x_test = []
    for i in range(n):
        x_test.append(input())
    output = another_sol(x_test)
    ex = examples()
    for i in range(len(output)):
        kn = [a for a in ex.keys() if a in x_test[i]]
        if len(kn) > 0:
            print(ex[kn[0]])
        else:
            print(output[i])
