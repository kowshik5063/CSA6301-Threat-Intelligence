{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyMdAHJ3YYMN89lzjNsGlEe/",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%2013.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "\n",
        "import hashlib\n",
        "\n",
        "def hash_file(path):\n",
        "    with open(path, \"rb\") as f:\n",
        "        return hashlib.sha256(f.read()).hexdigest()\n",
        "\n",
        "\n",
        "with open(\"original.txt\", \"w\") as f:\n",
        "    f.write(\"System32 backup data\")\n",
        "\n",
        "with open(\"copy.txt\", \"w\") as f:\n",
        "    f.write(\"System32 backup data\")\n",
        "\n",
        "with open(\"tampered.txt\", \"w\") as f:\n",
        "    f.write(\"System32 backup data - modified\")\n",
        "\n",
        "files = [\"original.txt\", \"copy.txt\", \"tampered.txt\"]\n",
        "\n",
        "hashes = {}\n",
        "\n",
        "for file in files:\n",
        "    hashes[file] = hash_file(file)\n",
        "\n",
        "baseline = hashes[\"original.txt\"]\n",
        "\n",
        "print(\"Baseline (original.txt):\", baseline)\n",
        "\n",
        "for file in files[1:]:\n",
        "    if hashes[file] == baseline:\n",
        "        status = \"IDENTICAL\"\n",
        "    else:\n",
        "        status = \"MODIFIED/TAMPERED\"\n",
        "\n",
        "    print(file + \":\", status)"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "txUjlDn0_jUa",
        "outputId": "22ef3d0f-7c76-4023-87af-3f0bca64c948"
      },
      "execution_count": 7,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Baseline (original.txt): 9ac62dc309d11594f1da0d160ded90eca26724461b1c55abeed293c23a0285d1\n",
            "copy.txt: IDENTICAL\n",
            "tampered.txt: MODIFIED/TAMPERED\n"
          ]
        }
      ]
    }
  ]
}