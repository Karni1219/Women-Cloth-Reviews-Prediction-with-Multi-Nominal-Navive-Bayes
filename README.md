{
  "cells": [
    {
      "cell_type": "markdown",
      "id": "4d63a162",
      "metadata": {
        "id": "4d63a162",
        "papermill": {
          "duration": 0.014903,
          "end_time": "2023-08-19T15:39:16.418631",
          "exception": false,
          "start_time": "2023-08-19T15:39:16.403728",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<u><h1>Women Cloth Reviews Prediction with Multi Nominal Navive Bayes</h1></u>\n",
        "<p>Multinomial Naïve Bayes algorithm is a probabilistic learning method that is mostly used in Natural Language Processing. It is also suitable for text classification with discrete feature. In this project it will be used to build a women cloth review prediction model.</p>"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "945d4c2c",
      "metadata": {
        "id": "945d4c2c",
        "papermill": {
          "duration": 0.015637,
          "end_time": "2023-08-19T15:39:16.448925",
          "exception": false,
          "start_time": "2023-08-19T15:39:16.433288",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Import Library<h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 1,
      "id": "e6c2b045",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:16.480703Z",
          "iopub.status.busy": "2023-08-19T15:39:16.479769Z",
          "iopub.status.idle": "2023-08-19T15:39:18.129202Z",
          "shell.execute_reply": "2023-08-19T15:39:18.128123Z"
        },
        "id": "e6c2b045",
        "papermill": {
          "duration": 1.668595,
          "end_time": "2023-08-19T15:39:18.131878",
          "exception": false,
          "start_time": "2023-08-19T15:39:16.463283",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "import numpy as np\n",
        "import matplotlib.pyplot as plt\n",
        "import seaborn as sns"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "3e89ea5a",
      "metadata": {
        "id": "3e89ea5a",
        "papermill": {
          "duration": 0.014488,
          "end_time": "2023-08-19T15:39:18.161352",
          "exception": false,
          "start_time": "2023-08-19T15:39:18.146864",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Import dataset<h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 2,
      "id": "85a33e4d",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:18.193904Z",
          "iopub.status.busy": "2023-08-19T15:39:18.193100Z",
          "iopub.status.idle": "2023-08-19T15:39:18.744414Z",
          "shell.execute_reply": "2023-08-19T15:39:18.743525Z"
        },
        "id": "85a33e4d",
        "papermill": {
          "duration": 0.571436,
          "end_time": "2023-08-19T15:39:18.747530",
          "exception": false,
          "start_time": "2023-08-19T15:39:18.176094",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "df = pd.read_csv(\"https://raw.githubusercontent.com/YBIFoundation/ProjectHub-MachineLearning/main/Women%20Clothing%20E-Commerce%20Review.csv\")"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "150a7c6d",
      "metadata": {
        "id": "150a7c6d",
        "papermill": {
          "duration": 0.014598,
          "end_time": "2023-08-19T15:39:18.780956",
          "exception": false,
          "start_time": "2023-08-19T15:39:18.766358",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Discribe Dataset<h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 3,
      "id": "01ceb3fb",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:18.814390Z",
          "iopub.status.busy": "2023-08-19T15:39:18.813404Z",
          "iopub.status.idle": "2023-08-19T15:39:18.841604Z",
          "shell.execute_reply": "2023-08-19T15:39:18.840549Z"
        },
        "id": "01ceb3fb",
        "outputId": "f6a3cd9c-9f59-489e-e387-1af2910dfc47",
        "papermill": {
          "duration": 0.048796,
          "end_time": "2023-08-19T15:39:18.845109",
          "exception": false,
          "start_time": "2023-08-19T15:39:18.796313",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 310
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "   Clothing ID  Age                    Title  \\\n",
              "0          767   33                      NaN   \n",
              "1         1080   34                      NaN   \n",
              "2         1077   60  Some major design flaws   \n",
              "3         1049   50         My favorite buy!   \n",
              "4          847   47         Flattering shirt   \n",
              "\n",
              "                                              Review  Rating  Recommended  \\\n",
              "0  Absolutely wonderful - silky and sexy and comf...       4            1   \n",
              "1  Love this dress!  it's sooo pretty.  i happene...       5            1   \n",
              "2  I had such high hopes for this dress and reall...       3            0   \n",
              "3  I love, love, love this jumpsuit. it's fun, fl...       5            1   \n",
              "4  This shirt is very flattering to all due to th...       5            1   \n",
              "\n",
              "   Positive Feedback        Division Department   Category  \n",
              "0                  0       Initmates   Intimate  Intimates  \n",
              "1                  4         General    Dresses    Dresses  \n",
              "2                  0         General    Dresses    Dresses  \n",
              "3                  0  General Petite    Bottoms      Pants  \n",
              "4                  6         General       Tops    Blouses  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-483bf561-682b-431b-a704-f09bd89e6068\" class=\"colab-df-container\">\n",
              "    <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Clothing ID</th>\n",
              "      <th>Age</th>\n",
              "      <th>Title</th>\n",
              "      <th>Review</th>\n",
              "      <th>Rating</th>\n",
              "      <th>Recommended</th>\n",
              "      <th>Positive Feedback</th>\n",
              "      <th>Division</th>\n",
              "      <th>Department</th>\n",
              "      <th>Category</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>767</td>\n",
              "      <td>33</td>\n",
              "      <td>NaN</td>\n",
              "      <td>Absolutely wonderful - silky and sexy and comf...</td>\n",
              "      <td>4</td>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>Initmates</td>\n",
              "      <td>Intimate</td>\n",
              "      <td>Intimates</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1080</td>\n",
              "      <td>34</td>\n",
              "      <td>NaN</td>\n",
              "      <td>Love this dress!  it's sooo pretty.  i happene...</td>\n",
              "      <td>5</td>\n",
              "      <td>1</td>\n",
              "      <td>4</td>\n",
              "      <td>General</td>\n",
              "      <td>Dresses</td>\n",
              "      <td>Dresses</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1077</td>\n",
              "      <td>60</td>\n",
              "      <td>Some major design flaws</td>\n",
              "      <td>I had such high hopes for this dress and reall...</td>\n",
              "      <td>3</td>\n",
              "      <td>0</td>\n",
              "      <td>0</td>\n",
              "      <td>General</td>\n",
              "      <td>Dresses</td>\n",
              "      <td>Dresses</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1049</td>\n",
              "      <td>50</td>\n",
              "      <td>My favorite buy!</td>\n",
              "      <td>I love, love, love this jumpsuit. it's fun, fl...</td>\n",
              "      <td>5</td>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>General Petite</td>\n",
              "      <td>Bottoms</td>\n",
              "      <td>Pants</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>847</td>\n",
              "      <td>47</td>\n",
              "      <td>Flattering shirt</td>\n",
              "      <td>This shirt is very flattering to all due to th...</td>\n",
              "      <td>5</td>\n",
              "      <td>1</td>\n",
              "      <td>6</td>\n",
              "      <td>General</td>\n",
              "      <td>Tops</td>\n",
              "      <td>Blouses</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-483bf561-682b-431b-a704-f09bd89e6068')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-483bf561-682b-431b-a704-f09bd89e6068 button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-483bf561-682b-431b-a704-f09bd89e6068');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-b1533a79-f0ec-4b9a-97ae-300bef0394ca\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-b1533a79-f0ec-4b9a-97ae-300bef0394ca')\"\n",
              "            title=\"Suggest charts\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const quickchartButtonEl =\n",
              "        document.querySelector('#' + key + ' button');\n",
              "      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "      quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "      try {\n",
              "        const charts = await google.colab.kernel.invokeFunction(\n",
              "            'suggestCharts', [key], {});\n",
              "      } catch (error) {\n",
              "        console.error('Error during call to suggestCharts:', error);\n",
              "      }\n",
              "      quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "      quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-b1533a79-f0ec-4b9a-97ae-300bef0394ca button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ]
          },
          "metadata": {},
          "execution_count": 3
        }
      ],
      "source": [
        "df.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 4,
      "id": "22c98579",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:18.880484Z",
          "iopub.status.busy": "2023-08-19T15:39:18.880005Z",
          "iopub.status.idle": "2023-08-19T15:39:18.954610Z",
          "shell.execute_reply": "2023-08-19T15:39:18.953755Z"
        },
        "id": "22c98579",
        "outputId": "1520089d-26c7-401e-bdc8-b40c6f2e4ad5",
        "papermill": {
          "duration": 0.09479,
          "end_time": "2023-08-19T15:39:18.958016",
          "exception": false,
          "start_time": "2023-08-19T15:39:18.863226",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "RangeIndex: 23486 entries, 0 to 23485\n",
            "Data columns (total 10 columns):\n",
            " #   Column             Non-Null Count  Dtype \n",
            "---  ------             --------------  ----- \n",
            " 0   Clothing ID        23486 non-null  int64 \n",
            " 1   Age                23486 non-null  int64 \n",
            " 2   Title              19676 non-null  object\n",
            " 3   Review             22641 non-null  object\n",
            " 4   Rating             23486 non-null  int64 \n",
            " 5   Recommended        23486 non-null  int64 \n",
            " 6   Positive Feedback  23486 non-null  int64 \n",
            " 7   Division           23472 non-null  object\n",
            " 8   Department         23472 non-null  object\n",
            " 9   Category           23472 non-null  object\n",
            "dtypes: int64(5), object(5)\n",
            "memory usage: 1.8+ MB\n"
          ]
        }
      ],
      "source": [
        "df.info()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 5,
      "id": "7daf7bc2",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:18.995955Z",
          "iopub.status.busy": "2023-08-19T15:39:18.994640Z",
          "iopub.status.idle": "2023-08-19T15:39:19.031641Z",
          "shell.execute_reply": "2023-08-19T15:39:19.030837Z"
        },
        "id": "7daf7bc2",
        "outputId": "cd83a074-8b99-4013-ffb0-535c5f469f63",
        "papermill": {
          "duration": 0.057323,
          "end_time": "2023-08-19T15:39:19.034567",
          "exception": false,
          "start_time": "2023-08-19T15:39:18.977244",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 300
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "        Clothing ID           Age        Rating   Recommended  \\\n",
              "count  23486.000000  23486.000000  23486.000000  23486.000000   \n",
              "mean     918.118709     43.198544      4.196032      0.822362   \n",
              "std      203.298980     12.279544      1.110031      0.382216   \n",
              "min        0.000000     18.000000      1.000000      0.000000   \n",
              "25%      861.000000     34.000000      4.000000      1.000000   \n",
              "50%      936.000000     41.000000      5.000000      1.000000   \n",
              "75%     1078.000000     52.000000      5.000000      1.000000   \n",
              "max     1205.000000     99.000000      5.000000      1.000000   \n",
              "\n",
              "       Positive Feedback  \n",
              "count       23486.000000  \n",
              "mean            2.535936  \n",
              "std             5.702202  \n",
              "min             0.000000  \n",
              "25%             0.000000  \n",
              "50%             1.000000  \n",
              "75%             3.000000  \n",
              "max           122.000000  "
            ],
            "text/html": [
              "\n",
              "  <div id=\"df-d29d264f-7e50-431e-b0ee-92b90ea63961\" class=\"colab-df-container\">\n",
              "    <div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>Clothing ID</th>\n",
              "      <th>Age</th>\n",
              "      <th>Rating</th>\n",
              "      <th>Recommended</th>\n",
              "      <th>Positive Feedback</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>count</th>\n",
              "      <td>23486.000000</td>\n",
              "      <td>23486.000000</td>\n",
              "      <td>23486.000000</td>\n",
              "      <td>23486.000000</td>\n",
              "      <td>23486.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>mean</th>\n",
              "      <td>918.118709</td>\n",
              "      <td>43.198544</td>\n",
              "      <td>4.196032</td>\n",
              "      <td>0.822362</td>\n",
              "      <td>2.535936</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>std</th>\n",
              "      <td>203.298980</td>\n",
              "      <td>12.279544</td>\n",
              "      <td>1.110031</td>\n",
              "      <td>0.382216</td>\n",
              "      <td>5.702202</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>min</th>\n",
              "      <td>0.000000</td>\n",
              "      <td>18.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>0.000000</td>\n",
              "      <td>0.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>25%</th>\n",
              "      <td>861.000000</td>\n",
              "      <td>34.000000</td>\n",
              "      <td>4.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>0.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>50%</th>\n",
              "      <td>936.000000</td>\n",
              "      <td>41.000000</td>\n",
              "      <td>5.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>1.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>75%</th>\n",
              "      <td>1078.000000</td>\n",
              "      <td>52.000000</td>\n",
              "      <td>5.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>3.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>max</th>\n",
              "      <td>1205.000000</td>\n",
              "      <td>99.000000</td>\n",
              "      <td>5.000000</td>\n",
              "      <td>1.000000</td>\n",
              "      <td>122.000000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>\n",
              "    <div class=\"colab-df-buttons\">\n",
              "\n",
              "  <div class=\"colab-df-container\">\n",
              "    <button class=\"colab-df-convert\" onclick=\"convertToInteractive('df-d29d264f-7e50-431e-b0ee-92b90ea63961')\"\n",
              "            title=\"Convert this dataframe to an interactive table.\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "  <svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\" viewBox=\"0 -960 960 960\">\n",
              "    <path d=\"M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z\"/>\n",
              "  </svg>\n",
              "    </button>\n",
              "\n",
              "  <style>\n",
              "    .colab-df-container {\n",
              "      display:flex;\n",
              "      gap: 12px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert {\n",
              "      background-color: #E8F0FE;\n",
              "      border: none;\n",
              "      border-radius: 50%;\n",
              "      cursor: pointer;\n",
              "      display: none;\n",
              "      fill: #1967D2;\n",
              "      height: 32px;\n",
              "      padding: 0 0 0 0;\n",
              "      width: 32px;\n",
              "    }\n",
              "\n",
              "    .colab-df-convert:hover {\n",
              "      background-color: #E2EBFA;\n",
              "      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "      fill: #174EA6;\n",
              "    }\n",
              "\n",
              "    .colab-df-buttons div {\n",
              "      margin-bottom: 4px;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert {\n",
              "      background-color: #3B4455;\n",
              "      fill: #D2E3FC;\n",
              "    }\n",
              "\n",
              "    [theme=dark] .colab-df-convert:hover {\n",
              "      background-color: #434B5C;\n",
              "      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);\n",
              "      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));\n",
              "      fill: #FFFFFF;\n",
              "    }\n",
              "  </style>\n",
              "\n",
              "    <script>\n",
              "      const buttonEl =\n",
              "        document.querySelector('#df-d29d264f-7e50-431e-b0ee-92b90ea63961 button.colab-df-convert');\n",
              "      buttonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "\n",
              "      async function convertToInteractive(key) {\n",
              "        const element = document.querySelector('#df-d29d264f-7e50-431e-b0ee-92b90ea63961');\n",
              "        const dataTable =\n",
              "          await google.colab.kernel.invokeFunction('convertToInteractive',\n",
              "                                                    [key], {});\n",
              "        if (!dataTable) return;\n",
              "\n",
              "        const docLinkHtml = 'Like what you see? Visit the ' +\n",
              "          '<a target=\"_blank\" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'\n",
              "          + ' to learn more about interactive tables.';\n",
              "        element.innerHTML = '';\n",
              "        dataTable['output_type'] = 'display_data';\n",
              "        await google.colab.output.renderOutput(dataTable, element);\n",
              "        const docLink = document.createElement('div');\n",
              "        docLink.innerHTML = docLinkHtml;\n",
              "        element.appendChild(docLink);\n",
              "      }\n",
              "    </script>\n",
              "  </div>\n",
              "\n",
              "\n",
              "<div id=\"df-3a3761ef-92a1-46bd-b1f2-c30091fb2ee4\">\n",
              "  <button class=\"colab-df-quickchart\" onclick=\"quickchart('df-3a3761ef-92a1-46bd-b1f2-c30091fb2ee4')\"\n",
              "            title=\"Suggest charts\"\n",
              "            style=\"display:none;\">\n",
              "\n",
              "<svg xmlns=\"http://www.w3.org/2000/svg\" height=\"24px\"viewBox=\"0 0 24 24\"\n",
              "     width=\"24px\">\n",
              "    <g>\n",
              "        <path d=\"M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z\"/>\n",
              "    </g>\n",
              "</svg>\n",
              "  </button>\n",
              "\n",
              "<style>\n",
              "  .colab-df-quickchart {\n",
              "      --bg-color: #E8F0FE;\n",
              "      --fill-color: #1967D2;\n",
              "      --hover-bg-color: #E2EBFA;\n",
              "      --hover-fill-color: #174EA6;\n",
              "      --disabled-fill-color: #AAA;\n",
              "      --disabled-bg-color: #DDD;\n",
              "  }\n",
              "\n",
              "  [theme=dark] .colab-df-quickchart {\n",
              "      --bg-color: #3B4455;\n",
              "      --fill-color: #D2E3FC;\n",
              "      --hover-bg-color: #434B5C;\n",
              "      --hover-fill-color: #FFFFFF;\n",
              "      --disabled-bg-color: #3B4455;\n",
              "      --disabled-fill-color: #666;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart {\n",
              "    background-color: var(--bg-color);\n",
              "    border: none;\n",
              "    border-radius: 50%;\n",
              "    cursor: pointer;\n",
              "    display: none;\n",
              "    fill: var(--fill-color);\n",
              "    height: 32px;\n",
              "    padding: 0;\n",
              "    width: 32px;\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart:hover {\n",
              "    background-color: var(--hover-bg-color);\n",
              "    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);\n",
              "    fill: var(--button-hover-fill-color);\n",
              "  }\n",
              "\n",
              "  .colab-df-quickchart-complete:disabled,\n",
              "  .colab-df-quickchart-complete:disabled:hover {\n",
              "    background-color: var(--disabled-bg-color);\n",
              "    fill: var(--disabled-fill-color);\n",
              "    box-shadow: none;\n",
              "  }\n",
              "\n",
              "  .colab-df-spinner {\n",
              "    border: 2px solid var(--fill-color);\n",
              "    border-color: transparent;\n",
              "    border-bottom-color: var(--fill-color);\n",
              "    animation:\n",
              "      spin 1s steps(1) infinite;\n",
              "  }\n",
              "\n",
              "  @keyframes spin {\n",
              "    0% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "      border-left-color: var(--fill-color);\n",
              "    }\n",
              "    20% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    30% {\n",
              "      border-color: transparent;\n",
              "      border-left-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    40% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-top-color: var(--fill-color);\n",
              "    }\n",
              "    60% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "    }\n",
              "    80% {\n",
              "      border-color: transparent;\n",
              "      border-right-color: var(--fill-color);\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "    90% {\n",
              "      border-color: transparent;\n",
              "      border-bottom-color: var(--fill-color);\n",
              "    }\n",
              "  }\n",
              "</style>\n",
              "\n",
              "  <script>\n",
              "    async function quickchart(key) {\n",
              "      const quickchartButtonEl =\n",
              "        document.querySelector('#' + key + ' button');\n",
              "      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.\n",
              "      quickchartButtonEl.classList.add('colab-df-spinner');\n",
              "      try {\n",
              "        const charts = await google.colab.kernel.invokeFunction(\n",
              "            'suggestCharts', [key], {});\n",
              "      } catch (error) {\n",
              "        console.error('Error during call to suggestCharts:', error);\n",
              "      }\n",
              "      quickchartButtonEl.classList.remove('colab-df-spinner');\n",
              "      quickchartButtonEl.classList.add('colab-df-quickchart-complete');\n",
              "    }\n",
              "    (() => {\n",
              "      let quickchartButtonEl =\n",
              "        document.querySelector('#df-3a3761ef-92a1-46bd-b1f2-c30091fb2ee4 button');\n",
              "      quickchartButtonEl.style.display =\n",
              "        google.colab.kernel.accessAllowed ? 'block' : 'none';\n",
              "    })();\n",
              "  </script>\n",
              "</div>\n",
              "    </div>\n",
              "  </div>\n"
            ]
          },
          "metadata": {},
          "execution_count": 5
        }
      ],
      "source": [
        "df.describe()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 6,
      "id": "9564147f",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.072290Z",
          "iopub.status.busy": "2023-08-19T15:39:19.071150Z",
          "iopub.status.idle": "2023-08-19T15:39:19.079559Z",
          "shell.execute_reply": "2023-08-19T15:39:19.078474Z"
        },
        "id": "9564147f",
        "outputId": "d0f0314c-49df-4e48-d827-0d03eb63a665",
        "papermill": {
          "duration": 0.028109,
          "end_time": "2023-08-19T15:39:19.081924",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.053815",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Index(['Clothing ID', 'Age', 'Title', 'Review', 'Rating', 'Recommended',\n",
              "       'Positive Feedback', 'Division', 'Department', 'Category'],\n",
              "      dtype='object')"
            ]
          },
          "metadata": {},
          "execution_count": 6
        }
      ],
      "source": [
        "df.columns"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "dee0e817",
      "metadata": {
        "id": "dee0e817",
        "papermill": {
          "duration": 0.015435,
          "end_time": "2023-08-19T15:39:19.114011",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.098576",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Data Preprocessing</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 7,
      "id": "015c6014",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.148168Z",
          "iopub.status.busy": "2023-08-19T15:39:19.147255Z",
          "iopub.status.idle": "2023-08-19T15:39:19.204527Z",
          "shell.execute_reply": "2023-08-19T15:39:19.203624Z"
        },
        "id": "015c6014",
        "outputId": "b6e8a120-4115-427f-a2e5-6b0f32bcb1d1",
        "papermill": {
          "duration": 0.07762,
          "end_time": "2023-08-19T15:39:19.207397",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.129777",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Clothing ID             0\n",
              "Age                     0\n",
              "Title                3810\n",
              "Review                845\n",
              "Rating                  0\n",
              "Recommended             0\n",
              "Positive Feedback       0\n",
              "Division               14\n",
              "Department             14\n",
              "Category               14\n",
              "dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 7
        }
      ],
      "source": [
        "df.isna().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 8,
      "id": "67eb44da",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.240690Z",
          "iopub.status.busy": "2023-08-19T15:39:19.240324Z",
          "iopub.status.idle": "2023-08-19T15:39:19.262328Z",
          "shell.execute_reply": "2023-08-19T15:39:19.259676Z"
        },
        "id": "67eb44da",
        "papermill": {
          "duration": 0.042124,
          "end_time": "2023-08-19T15:39:19.265426",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.223302",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "df[df['Review']== \"\"] = np.NaN\n",
        "df['Review'].fillna(\"No Review\", inplace= True)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 9,
      "id": "8c1d0ed2",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.301115Z",
          "iopub.status.busy": "2023-08-19T15:39:19.300416Z",
          "iopub.status.idle": "2023-08-19T15:39:19.307955Z",
          "shell.execute_reply": "2023-08-19T15:39:19.307147Z"
        },
        "id": "8c1d0ed2",
        "outputId": "3dfed126-5558-4436-bae9-3c46fcc560c4",
        "papermill": {
          "duration": 0.026999,
          "end_time": "2023-08-19T15:39:19.310232",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.283233",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0        Absolutely wonderful - silky and sexy and comf...\n",
              "1        Love this dress!  it's sooo pretty.  i happene...\n",
              "2        I had such high hopes for this dress and reall...\n",
              "3        I love, love, love this jumpsuit. it's fun, fl...\n",
              "4        This shirt is very flattering to all due to th...\n",
              "                               ...                        \n",
              "23481    I was very happy to snag this dress at such a ...\n",
              "23482    It reminds me of maternity clothes. soft, stre...\n",
              "23483    This fit well, but the top was very see throug...\n",
              "23484    I bought this dress for a wedding i have this ...\n",
              "23485    This dress in a lovely platinum is feminine an...\n",
              "Name: Review, Length: 23486, dtype: object"
            ]
          },
          "metadata": {},
          "execution_count": 9
        }
      ],
      "source": [
        "df['Review']"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 10,
      "id": "6e2b8588",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.344233Z",
          "iopub.status.busy": "2023-08-19T15:39:19.343565Z",
          "iopub.status.idle": "2023-08-19T15:39:19.390280Z",
          "shell.execute_reply": "2023-08-19T15:39:19.389471Z"
        },
        "id": "6e2b8588",
        "outputId": "3b81d912-ce26-41d1-b458-9b13bb882703",
        "papermill": {
          "duration": 0.066255,
          "end_time": "2023-08-19T15:39:19.392516",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.326261",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Clothing ID             0\n",
              "Age                     0\n",
              "Title                3810\n",
              "Review                  0\n",
              "Rating                  0\n",
              "Recommended             0\n",
              "Positive Feedback       0\n",
              "Division               14\n",
              "Department             14\n",
              "Category               14\n",
              "dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 10
        }
      ],
      "source": [
        "df.isna().sum()"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "ade212ea",
      "metadata": {
        "id": "ade212ea",
        "papermill": {
          "duration": 0.015704,
          "end_time": "2023-08-19T15:39:19.424443",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.408739",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Define target(y) and feature(X)</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 11,
      "id": "18a7ba64",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.458617Z",
          "iopub.status.busy": "2023-08-19T15:39:19.457901Z",
          "iopub.status.idle": "2023-08-19T15:39:19.464353Z",
          "shell.execute_reply": "2023-08-19T15:39:19.463276Z"
        },
        "id": "18a7ba64",
        "outputId": "6499b38c-8387-4c7a-fd29-0601e780e5d1",
        "papermill": {
          "duration": 0.026357,
          "end_time": "2023-08-19T15:39:19.466811",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.440454",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "Index(['Clothing ID', 'Age', 'Title', 'Review', 'Rating', 'Recommended',\n",
              "       'Positive Feedback', 'Division', 'Department', 'Category'],\n",
              "      dtype='object')"
            ]
          },
          "metadata": {},
          "execution_count": 11
        }
      ],
      "source": [
        "df.columns"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 12,
      "id": "7e6b6402",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.501533Z",
          "iopub.status.busy": "2023-08-19T15:39:19.501094Z",
          "iopub.status.idle": "2023-08-19T15:39:19.515452Z",
          "shell.execute_reply": "2023-08-19T15:39:19.514307Z"
        },
        "id": "7e6b6402",
        "outputId": "cb9df6d9-c9ed-47c8-8850-160600a7fd12",
        "papermill": {
          "duration": 0.034878,
          "end_time": "2023-08-19T15:39:19.518085",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.483207",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "1.0    18208\n",
              "0.0     5278\n",
              "Name: Rating, dtype: int64"
            ]
          },
          "metadata": {},
          "execution_count": 12
        }
      ],
      "source": [
        "#............................................................\n",
        "df.replace({'Rating': { 1:0, 2:0, 3:0, 4:1, 5:1 }}, inplace=True)\n",
        "y = df['Rating']\n",
        "x = df['Review']\n",
        "df['Rating'].value_counts()"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "3fc98cb1",
      "metadata": {
        "id": "3fc98cb1",
        "papermill": {
          "duration": 0.016332,
          "end_time": "2023-08-19T15:39:19.550873",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.534541",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Train_test_split</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 13,
      "id": "71c98435",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.586429Z",
          "iopub.status.busy": "2023-08-19T15:39:19.585627Z",
          "iopub.status.idle": "2023-08-19T15:39:19.881248Z",
          "shell.execute_reply": "2023-08-19T15:39:19.880062Z"
        },
        "id": "71c98435",
        "papermill": {
          "duration": 0.316796,
          "end_time": "2023-08-19T15:39:19.884146",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.567350",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "from sklearn.model_selection import train_test_split\n",
        "x_train, x_test, y_train, y_test = train_test_split(x, y, train_size=0.7, random_state=2529)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 14,
      "id": "2d779453",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.919045Z",
          "iopub.status.busy": "2023-08-19T15:39:19.918383Z",
          "iopub.status.idle": "2023-08-19T15:39:19.925761Z",
          "shell.execute_reply": "2023-08-19T15:39:19.924669Z"
        },
        "id": "2d779453",
        "outputId": "24464c27-77f1-49cc-98d3-ef7badfc6b15",
        "papermill": {
          "duration": 0.027457,
          "end_time": "2023-08-19T15:39:19.928025",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.900568",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "((16440,), (7046,), (16440,), (7046,))"
            ]
          },
          "metadata": {},
          "execution_count": 14
        }
      ],
      "source": [
        "x_train.shape,x_test.shape,y_train.shape,y_test.shape"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "0c3140e4",
      "metadata": {
        "id": "0c3140e4",
        "papermill": {
          "duration": 0.016252,
          "end_time": "2023-08-19T15:39:19.960970",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.944718",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3> - Get Feature Test Conversion to Tokens</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 15,
      "id": "c9d8ff13",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:19.996002Z",
          "iopub.status.busy": "2023-08-19T15:39:19.995541Z",
          "iopub.status.idle": "2023-08-19T15:39:24.264746Z",
          "shell.execute_reply": "2023-08-19T15:39:24.263628Z"
        },
        "id": "c9d8ff13",
        "outputId": "3eebf9c0-46bf-4d54-f904-e11ceba5960a",
        "papermill": {
          "duration": 4.289798,
          "end_time": "2023-08-19T15:39:24.267215",
          "exception": false,
          "start_time": "2023-08-19T15:39:19.977417",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array(['00 big', '00 dresses', '00 fit', ..., 'zipper zip',\n",
              "       'zippered pockets', 'zippers buttons'], dtype=object)"
            ]
          },
          "metadata": {},
          "execution_count": 15
        }
      ],
      "source": [
        "from sklearn.feature_extraction.text import CountVectorizer\n",
        "\n",
        "cv = CountVectorizer(lowercase=True, analyzer='word', ngram_range=(2, 3), stop_words='english', max_features=50000)\n",
        "x_train = cv.fit_transform(x_train)\n",
        "cv.get_feature_names_out()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 16,
      "id": "936d4ca9",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:24.304044Z",
          "iopub.status.busy": "2023-08-19T15:39:24.303620Z",
          "iopub.status.idle": "2023-08-19T15:39:24.926060Z",
          "shell.execute_reply": "2023-08-19T15:39:24.924742Z"
        },
        "id": "936d4ca9",
        "outputId": "ea9be0d1-f228-4958-d8e3-4b47e9b63ae2",
        "papermill": {
          "duration": 0.644242,
          "end_time": "2023-08-19T15:39:24.929001",
          "exception": false,
          "start_time": "2023-08-19T15:39:24.284759",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([[0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       ...,\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0]])"
            ]
          },
          "metadata": {},
          "execution_count": 16
        }
      ],
      "source": [
        "x_train.toarray()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 17,
      "id": "64d79a9d",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:24.964864Z",
          "iopub.status.busy": "2023-08-19T15:39:24.964464Z",
          "iopub.status.idle": "2023-08-19T15:39:26.728753Z",
          "shell.execute_reply": "2023-08-19T15:39:26.727762Z"
        },
        "id": "64d79a9d",
        "papermill": {
          "duration": 1.78526,
          "end_time": "2023-08-19T15:39:26.731462",
          "exception": false,
          "start_time": "2023-08-19T15:39:24.946202",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "x_test = cv.fit_transform(x_test)\n"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 18,
      "id": "9f526944",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:26.767214Z",
          "iopub.status.busy": "2023-08-19T15:39:26.766608Z",
          "iopub.status.idle": "2023-08-19T15:39:26.850202Z",
          "shell.execute_reply": "2023-08-19T15:39:26.849154Z"
        },
        "id": "9f526944",
        "outputId": "4d5c087f-5ed8-4847-d5b4-fdd74759242e",
        "papermill": {
          "duration": 0.104064,
          "end_time": "2023-08-19T15:39:26.852403",
          "exception": false,
          "start_time": "2023-08-19T15:39:26.748339",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array(['00 fits', '00 fits perfectly', '00 petite', ..., 'zipper little',\n",
              "       'zipper pockets', 'zipper wouldn'], dtype=object)"
            ]
          },
          "metadata": {},
          "execution_count": 18
        }
      ],
      "source": [
        "cv.get_feature_names_out()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 19,
      "id": "155bc252",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:26.889514Z",
          "iopub.status.busy": "2023-08-19T15:39:26.888754Z",
          "iopub.status.idle": "2023-08-19T15:39:27.151723Z",
          "shell.execute_reply": "2023-08-19T15:39:27.150592Z"
        },
        "id": "155bc252",
        "outputId": "8b47cbaa-b68c-4c20-d282-9dbf1afc249f",
        "papermill": {
          "duration": 0.284334,
          "end_time": "2023-08-19T15:39:27.154161",
          "exception": false,
          "start_time": "2023-08-19T15:39:26.869827",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([[0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       ...,\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0],\n",
              "       [0, 0, 0, ..., 0, 0, 0]])"
            ]
          },
          "metadata": {},
          "execution_count": 19
        }
      ],
      "source": [
        "x_test.toarray()"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "7220f338",
      "metadata": {
        "id": "7220f338",
        "papermill": {
          "duration": 0.016954,
          "end_time": "2023-08-19T15:39:27.188753",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.171799",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Get Model Train</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 20,
      "id": "a535fe84",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.224997Z",
          "iopub.status.busy": "2023-08-19T15:39:27.224565Z",
          "iopub.status.idle": "2023-08-19T15:39:27.238761Z",
          "shell.execute_reply": "2023-08-19T15:39:27.237562Z"
        },
        "id": "a535fe84",
        "papermill": {
          "duration": 0.035574,
          "end_time": "2023-08-19T15:39:27.241571",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.205997",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "from sklearn.naive_bayes import MultinomialNB\n",
        "model = MultinomialNB()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 21,
      "id": "ae3dfc6c",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.278353Z",
          "iopub.status.busy": "2023-08-19T15:39:27.277903Z",
          "iopub.status.idle": "2023-08-19T15:39:27.302946Z",
          "shell.execute_reply": "2023-08-19T15:39:27.301898Z"
        },
        "id": "ae3dfc6c",
        "outputId": "aac7b945-40f8-4d03-fcc5-e3aa0af0c41c",
        "papermill": {
          "duration": 0.046319,
          "end_time": "2023-08-19T15:39:27.305454",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.259135",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 74
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "MultinomialNB()"
            ],
            "text/html": [
              "<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-1\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>MultinomialNB()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-1\" type=\"checkbox\" checked><label for=\"sk-estimator-id-1\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">MultinomialNB</label><div class=\"sk-toggleable__content\"><pre>MultinomialNB()</pre></div></div></div></div></div>"
            ]
          },
          "metadata": {},
          "execution_count": 21
        }
      ],
      "source": [
        "model.fit(x_train,y_train)"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "4f9b3df8",
      "metadata": {
        "id": "4f9b3df8",
        "papermill": {
          "duration": 0.017307,
          "end_time": "2023-08-19T15:39:27.340435",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.323128",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Model Prediction</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 22,
      "id": "61e8a269",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.377293Z",
          "iopub.status.busy": "2023-08-19T15:39:27.376875Z",
          "iopub.status.idle": "2023-08-19T15:39:27.390423Z",
          "shell.execute_reply": "2023-08-19T15:39:27.389360Z"
        },
        "id": "61e8a269",
        "outputId": "37e73b17-3a55-46c0-d7ce-6481186c7ff7",
        "papermill": {
          "duration": 0.034582,
          "end_time": "2023-08-19T15:39:27.392693",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.358111",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([1., 0., 1., ..., 0., 1., 1.])"
            ]
          },
          "metadata": {},
          "execution_count": 22
        }
      ],
      "source": [
        "y_pred = model.predict(x_test)\n",
        "y_pred"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 23,
      "id": "82ae603d",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.430418Z",
          "iopub.status.busy": "2023-08-19T15:39:27.429584Z",
          "iopub.status.idle": "2023-08-19T15:39:27.436743Z",
          "shell.execute_reply": "2023-08-19T15:39:27.435854Z"
        },
        "id": "82ae603d",
        "outputId": "74c74982-1d05-4551-b4e5-48756b0587fa",
        "papermill": {
          "duration": 0.028778,
          "end_time": "2023-08-19T15:39:27.439107",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.410329",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "(7046,)"
            ]
          },
          "metadata": {},
          "execution_count": 23
        }
      ],
      "source": [
        "y_pred.shape"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "a8303f33",
      "metadata": {
        "id": "a8303f33",
        "papermill": {
          "duration": 0.01765,
          "end_time": "2023-08-19T15:39:27.474450",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.456800",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Get Probability of Each Predicted Class</h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 24,
      "id": "2eb177b5",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.512266Z",
          "iopub.status.busy": "2023-08-19T15:39:27.511814Z",
          "iopub.status.idle": "2023-08-19T15:39:27.523818Z",
          "shell.execute_reply": "2023-08-19T15:39:27.522744Z"
        },
        "id": "2eb177b5",
        "outputId": "8648c887-b7c6-4349-f76b-2059345e9f12",
        "papermill": {
          "duration": 0.033881,
          "end_time": "2023-08-19T15:39:27.526248",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.492367",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([[0.00681789, 0.99318211],\n",
              "       [0.95449908, 0.04550092],\n",
              "       [0.00480856, 0.99519144],\n",
              "       ...,\n",
              "       [0.82969833, 0.17030167],\n",
              "       [0.07093417, 0.92906583],\n",
              "       [0.4807814 , 0.5192186 ]])"
            ]
          },
          "metadata": {},
          "execution_count": 24
        }
      ],
      "source": [
        "model.predict_proba(x_test)"
      ]
    },
    {
      "cell_type": "markdown",
      "id": "3d47d96b",
      "metadata": {
        "id": "3d47d96b",
        "papermill": {
          "duration": 0.017711,
          "end_time": "2023-08-19T15:39:27.562044",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.544333",
          "status": "completed"
        },
        "tags": []
      },
      "source": [
        "<h3>- Model Accuracy </h3>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 25,
      "id": "e16fd98b",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.599919Z",
          "iopub.status.busy": "2023-08-19T15:39:27.599499Z",
          "iopub.status.idle": "2023-08-19T15:39:27.604219Z",
          "shell.execute_reply": "2023-08-19T15:39:27.603059Z"
        },
        "id": "e16fd98b",
        "papermill": {
          "duration": 0.026721,
          "end_time": "2023-08-19T15:39:27.606752",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.580031",
          "status": "completed"
        },
        "tags": []
      },
      "outputs": [],
      "source": [
        "from sklearn.metrics import confusion_matrix, accuracy_score,classification_report"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 26,
      "id": "97698fdf",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.645123Z",
          "iopub.status.busy": "2023-08-19T15:39:27.644013Z",
          "iopub.status.idle": "2023-08-19T15:39:27.663423Z",
          "shell.execute_reply": "2023-08-19T15:39:27.662339Z"
        },
        "id": "97698fdf",
        "outputId": "14e46eee-7b80-4653-b22d-955eae97ed07",
        "papermill": {
          "duration": 0.041094,
          "end_time": "2023-08-19T15:39:27.665733",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.624639",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([[ 727, 2476],\n",
              "       [ 803, 3040]])"
            ]
          },
          "metadata": {},
          "execution_count": 26
        }
      ],
      "source": [
        "confusion_matrix(y_pred,y_test)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 27,
      "id": "9f7853dc",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.704025Z",
          "iopub.status.busy": "2023-08-19T15:39:27.703587Z",
          "iopub.status.idle": "2023-08-19T15:39:27.712928Z",
          "shell.execute_reply": "2023-08-19T15:39:27.711788Z"
        },
        "id": "9f7853dc",
        "outputId": "d3c2f73b-9cde-4ad3-8fcc-9f0e5b2bd6a3",
        "papermill": {
          "duration": 0.031497,
          "end_time": "2023-08-19T15:39:27.715222",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.683725",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.5346295770650015"
            ]
          },
          "metadata": {},
          "execution_count": 27
        }
      ],
      "source": [
        "accuracy_score(y_pred,y_test)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": 28,
      "id": "a8e34797",
      "metadata": {
        "execution": {
          "iopub.execute_input": "2023-08-19T15:39:27.754021Z",
          "iopub.status.busy": "2023-08-19T15:39:27.753236Z",
          "iopub.status.idle": "2023-08-19T15:39:27.783290Z",
          "shell.execute_reply": "2023-08-19T15:39:27.782097Z"
        },
        "id": "a8e34797",
        "outputId": "fa98ecb2-ebff-4e6f-bdf6-23e2d4ac8d98",
        "papermill": {
          "duration": 0.052143,
          "end_time": "2023-08-19T15:39:27.785730",
          "exception": false,
          "start_time": "2023-08-19T15:39:27.733587",
          "status": "completed"
        },
        "tags": [],
        "colab": {
          "base_uri": "https://localhost:8080/"
        }
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "              precision    recall  f1-score   support\n",
            "\n",
            "         0.0       0.48      0.23      0.31      3203\n",
            "         1.0       0.55      0.79      0.65      3843\n",
            "\n",
            "    accuracy                           0.53      7046\n",
            "   macro avg       0.51      0.51      0.48      7046\n",
            "weighted avg       0.52      0.53      0.49      7046\n",
            "\n"
          ]
        }
      ],
      "source": [
        "print(classification_report(y_pred,y_test))"
      ]
    }
  ],
  "metadata": {
    "kernelspec": {
      "display_name": "Python 3",
      "language": "python",
      "name": "python3"
    },
    "language_info": {
      "codemirror_mode": {
        "name": "ipython",
        "version": 3
      },
      "file_extension": ".py",
      "mimetype": "text/x-python",
      "name": "python",
      "nbconvert_exporter": "python",
      "pygments_lexer": "ipython3",
      "version": "3.10.12"
    },
    "papermill": {
      "default_parameters": {},
      "duration": 24.246915,
      "end_time": "2023-08-19T15:39:29.028316",
      "environment_variables": {},
      "exception": null,
      "input_path": "__notebook__.ipynb",
      "output_path": "__notebook__.ipynb",
      "parameters": {},
      "start_time": "2023-08-19T15:39:04.781401",
      "version": "2.4.0"
    },
    "colab": {
      "provenance": []
    }
  },
  "nbformat": 4,
  "nbformat_minor": 5
}
