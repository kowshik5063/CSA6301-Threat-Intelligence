{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyNTGjR969faIEKEgDG5xJZ9",
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
        "<a href=\"https://colab.research.google.com/github/kowshik5063/CSA6301-Threat-Intelligence/blob/main/Experiment%208.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "import hashlib\n",
        "\n",
        "stolen_hash = hashlib.sha256(\"letmein\".encode()).hexdigest()\n",
        "\n",
        "wordlist = [\"123456\", \"password\", \"admin\", \"letmein\", \"qwerty\"]\n",
        "\n",
        "print(\"Attempting dictionary attack on stolen hash...\")\n",
        "\n",
        "for word in wordlist:\n",
        "    guess_hash = hashlib.sha256(word.encode()).hexdigest()\n",
        "\n",
        "    if guess_hash == stolen_hash:\n",
        "        print(\"Password cracked:\", word)\n",
        "        break\n",
        "else:\n",
        "    print(\"Password not found in wordlist.\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "lpSbP8XY9uZG",
        "outputId": "d18b96b4-37cc-4630-acec-ab32fdc9d133"
      },
      "execution_count": 2,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Attempting dictionary attack on stolen hash...\n",
            "Password cracked: letmein\n"
          ]
        }
      ]
    }
  ]
}